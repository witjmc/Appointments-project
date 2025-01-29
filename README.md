
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



        - @nrwl/react, @nrwl/vue 프레임워크를 설치하지 않아서, node 로 설치해야함
    


        o 애플리케이션 폴더 생성

                      # npx nx generate @nrwl/workspace:application <your-app-name:appointment-app>


                     
                      # npx nx generate @nrwl/node:application <your-app-name> --frontendFramework=none --verbose




         
     o 프로젝트 의존성 확인
     

                        # npx nx show project appointment-app
  



     o 애플리케이션 실행
     

                         # npx nx run appointment-app:serve






      - tsconfig.base.json/ tsconfig.json  파일에 속성 맞추기:
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

  
  3. typescript 패키지 설치
     
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
                      group VARCHAR2(100) NOT NULL,        --전문 분야 이름 (예: "심장과", "내과" 등)
                      description VARCHAR2(255)           -- 전문 분야 설명
                  );


                  
                
