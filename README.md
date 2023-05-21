# jenkin-101

ใช้กับ repo public

```
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/dudkinox/jenkin-101'
            }
        }
        stage('Docker image') {
            steps {
                sh "echo Docker image"
            }
        }
        stage('Deploy') {
            steps {
                sh "echo Deploy"
            }
        }
        stage('Discord noti') {
            steps {
                sh "echo Discord noti"
            }
        }
    }
}
```

# จากนั้นผูก webhook กับ repo

ถ้าต้องการใช้ commit จาก github มาแสดง และส่ง แจ้งเตือน discord

````
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/dudkinox/jenkin-giude-by-guitar'
            }
        }
        stage('Docker image') {
            steps {
                sh "echo Docker image"
            }
        }
        stage('Deploy') {
            steps {
                sh "echo Deploy"
            }
        }
        stage('Send to Discord') {
            steps {
                script {
                    // อ่านข้อมูลของ commit ล่าสุดจาก Git
                    def commitMessage = sh(script: 'git log -1 --pretty=%B', returnStdout: true).trim()

                    // สร้าง JSON payload สำหรับส่งไปยัง Discord webhook
                    def payload = [
                        'content': commitMessage
                    ]

                    // ทำการส่งข้อมูลไปยัง Discord webhook โดยใช้คำสั่ง curl
                    sh """
                    curl --location 'https://discord.com/api/webhooks/1109545219998888019/HWCYJ7BNC-ziImku1qsTHMO4Je6RGtA1Jl49RZWnWbE7floi2mIZh1Iv1eqcno4cUjLx' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: __cfruid=5a111c5df2e500e6b058b3960f9fafb329b34c36-1684606808; __dcfduid=7cb24e7aee3911edbb4bbe49305c5a94; __sdcfduid=7cb24e7aee3911edbb4bbe49305c5a942582922a9f22eacbd469647c2105ecf4db8042864bc0506d602020917cbe7923' \
--data-urlencode 'content=เสร็จแล้ว Deploy :guitar: \n ```${payload.content}```'
                """
                }
            }
        }
    }
}
````
