
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
                     
#  



