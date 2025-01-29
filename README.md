# Appointments-project

-- 사용자 테이블

CREATE TABLE users (
    id NUMBER PRIMARY KEY,               -- 사용자 ID (기본 키)
    username VARCHAR2(100) UNIQUE,       -- 사용자 이름 (로그인 아이디)
    password VARCHAR2(255),              -- 암호 (비밀번호)
    role VARCHAR2(50),                   -- 역할 (admin, doctor, patient 등)
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  -- 생성일
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- 수정일
);

-- 전문 분야 테이블

CREATE TABLE specializations (
    id NUMBER PRIMARY KEY,               --전문 분야 ID
    group VARCHAR2(100) NOT NULL,        --전문 분야 이름 (예: "심장과", "내과" 등)
    description VARCHAR2(255)           -- 전문 분야 설명
);

-- 환자 테이블

CREATE TABLE patients (
    id NUMBER PRIMARY KEY,               -- 환자 테이블 ID 
    user_id NUMBER,                      -- users 테이블의 id 참조
    date_of_birth DATE,                   -- 생년월일
    FOREIGN KEY (user_id) REFERENCES users(id)  -- 외래 키: `users` 테이블 참조
);

-- 의사 테이블

CREATE TABLE doctors (
    id NUMBER PRIMARY KEY,               -- 의사 테이블 ID 
    user_id NUMBER,                      -- users 테이블의 id 참조
    specialization_id NUMBER ,     -- 전문 분야 ID (specializations 테이블 참조)
    FOREIGN KEY (specialization_id) REFERENCES specializations(id)  -- 외래 키: `specializations` 테이블 참조
    FOREIGN KEY (user_id) REFERENCES users(id)  -- 외래 키: `users` 테이블 참조
);



-- 예약 테이블

CREATE TABLE appointments (
    id NUMBER PRIMARY KEY,               -- 예약 ID
    patient_id NUMBER,                    -- 환자 ID (환자 테이블의 id 참조)
    doctor_id NUMBER,                     -- 의사 ID (의사 테이블의 id 참조)
    specialization_id NUMBER,             -- 전문 분야 ID (specializations 테이블의 id 참조)
    appointment_date DATE,                 -- 예약 일시
    status VARCHAR2(50),                   -- 예약 상태 (예: 'pending', 'confirmed', 'cancelled')
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- 생성일
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- 수정일
    created_by NUMBER,                    -- 예약을 생성한 사용자 (관리자 또는 환자)
    FOREIGN KEY (patient_id) REFERENCES patients(id),  -- 외래 키: `patients` 테이블 참조
    FOREIGN KEY (doctor_id) REFERENCES doctors(id),   -- 외래 키: `doctors` 테이블 참조
    FOREIGN KEY (specialization_id) REFERENCES specializations(id)  -- 외래 키: `specializations` 테이블 참조
    FOREIGN KEY (created_by) REFERENCES users(id)   -- 예약을 생성한 사용자의 외래 키  
);



