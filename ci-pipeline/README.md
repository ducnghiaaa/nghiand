# CI Pipeline with Jenkins 

## Introduction
This project etablishes a continuos integration (CI) automation process using Jenkins to ensure code quality and manage artifacts effectively.

## Architecture
<img width="933" height="499" alt="image" src="https://github.com/user-attachments/assets/f87a6ad0-510d-457e-996d-c3d4e99b9037" />

## Workflow Details
```mermaid
sequenceDiagram
    participant Dev as Developer
    participant GitHub as GitHub Repository
    participant Jenkins as Jenkins Server
    participant SonarQube as SonarQube Server
    participant Nexus as Nexus Repository Manager

    Dev->>GitHub: 1. Push Code (ví dụ: git push)
    GitHub-->>Jenkins: 2. Kích hoạt Webhook (hoặc polling)
    
    Jenkins->>GitHub: 3. Fetch Code (git clone/pull)

    Jenkins->>Jenkins: 4. Build Code (ví dụ: mvn clean compile)

    Jenkins->>Jenkins: 5. Run Unit Tests (ví dụ: mvn test)

    Jenkins->>SonarQube: 6. Gửi báo cáo phân tích Code (ví dụ: mvn sonar:sonar)
    SonarQube-->>Jenkins: 7. Trả về kết quả phân tích & Quality Gate

    alt Quality Gate Pass
        Jenkins->>Nexus: 8. Upload Artifact (ví dụ: my-app.jar)
        Nexus-->>Jenkins: 9. Xác nhận Artifact được lưu trữ
        Jenkins-->>Dev: 10. Pipeline hoàn tất thành công
    else Quality Gate Fail
        Jenkins--xDev: 8. Pipeline thất bại (ví dụ: do lỗi bảo mật, code smell cao)
    end
```

## Tech Stack
- CI Tool: Jenkins
- Source Control: GitHub
- Static Code Analysis: SonarQube
- Artifact Management: Nexus OSS
- Build Tools: Maven

## Install and using
- System req: jenkins, nexus, sonarqube, firewall, plugins
- Intergrate: nexus, sonarqube
- Write Pipeline script
- Set notification
