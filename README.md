
# nx 모노레포 관리 설치 순서
  1) 워크스페이스 생성 
            
                       # npx create-nx-workspace@latest <workspace-name:project-appiontment> 

      -stack/framwork : None ( Configures a TypeScript/JavaScript monorepo)

  2) 애플리케이션 생성 

       o 폴더 안에서만 설치
       
                      # npm install --save-dev nx

        o nrwl/workspace 패키지 플러그인 확인
     
                      # npm list @nrwl/workspace


        o 없으면, 설치
     
                      # npm install --save-dev @nrwl/workspace @nrwl/node



      -@nrwl/react, @nrwl/vue 프레임워크를 설치하지 않아서, node 로 설치해야함
    


        o 애플리케이션 폴더 생성

                      # npx nx generate @nrwl/workspace:application <your-app-name:appointment-app>


                     
                      # npx nx generate @nrwl/node:application <your-app-name> --frontendFramework=none --verbose




         
     o 프로젝트 의존성 확인
     

                        # npx nx show project appointment-app
  



     o 애플리케이션 실행
     

                         # npx nx run appointment-app:serve






    -tsconfig.base.json/ tsconfig.json  파일에 속성 맞추기:
             "module": "NodeNext",
             "moduleResolution": "NodeNext",



  4)  라이브러리 생성

                      # npx nx generate @nrwl/workspace:library shared-utils

                      # npx nx generate @nrwl/node:library shared-utils

  5) 빌드
     
                      # npx nx run appointment-app:build

              
  6) 테스트
     
                      # npx nx run appointment-app:test
     
          

         
                     
# 데이터베이스 설치 : Oracle 

  1. 프로젝트 위치
     
                      #cd appiontment-app

     
  2.  oracle 라이브러리 설치
     
                      # npm install oracledb

                      # npm install oracledb@latest


  
  4. typescript 패키지 설치
     
                      # npm install --save-dev @types/oracledb

            

# 데이터베이스 테이블

   1. 사용자 테이블

                  
                  CREATE TABLE users (
                      id NUMBER PRIMARY KEY,               -- 사용자 ID (기본 키)
                      username VARCHAR2(100) UNIQUE,       -- 사용자 이름 (로그인 아이디)
                      password VARCHAR2(255),              -- 암호 (비밀번호)
                      role VARCHAR2(50),                   -- 역할 (admin, doctor, patient 등)
                      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  -- 생성일
                      updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- 수정일
                  );





  2. 전문 분야 테이블



                  CREATE TABLE specializations (
                      id NUMBER PRIMARY KEY,               --전문 분야 ID
                      spe_group VARCHAR2(100) NOT NULL,        --전문 분야 이름 (예: "심장과", "내과" 등)
                      description VARCHAR2(255)           -- 전문 분야 설명
                  );



  3. 환자 테이블


                CREATE TABLE patients (
                    id NUMBER PRIMARY KEY,               -- 환자 테이블 ID 
                    user_id NUMBER,                      -- users 테이블의 id 참조
                    date_of_birth DATE,                   -- 생년월일
                    FOREIGN KEY (user_id) REFERENCES users(id)  -- 외래 키: `users` 테이블 참조
                  );
                   
                  

  4. 의사 테이블


                CREATE TABLE doctors (
                    id NUMBER PRIMARY KEY,               -- 의사 테이블 ID 
                    user_id NUMBER,                      -- users 테이블의 id 참조
                    specialization_id NUMBER ,     -- 전문 분야 ID (specializations 테이블 참조)
                    FOREIGN KEY (specialization_id) REFERENCES specializations(id),  -- 외래 키: `specializations` 테이블 참조
                    FOREIGN KEY (user_id) REFERENCES users(id)  -- 외래 키: `users` 테이블 참조
                );


  5. 예약 테이블


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
                    FOREIGN KEY (specialization_id) REFERENCES specializations(id),  -- 외래 키: `specializations` 테이블 참조
                    FOREIGN KEY (created_by) REFERENCES users(id)   -- 예약을 생성한 사용자의 외래 키  
                  );

              ![image](https://github.com/user-attachments/assets/601ca4dc-d746-488f-be69-a5a8c408e2f1)




             
