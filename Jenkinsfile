
def setBuildDisplayName() {
    // 定义日期时间格式：年-月-日 时:分:秒
    def dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
    def currentDateTime = dateFormat.format(new Date())
    def description = currentBuild.displayName + "\n" + "$currentDateTime"
    currentBuild.description = "时间: $currentDateTime" + "\n" + "分支: xx" + "\n" + "环境: xx"
}


pipeline {
    agent any

    stages {
        stage('初始化/ initialization') {
            steps {
                echo '初始化'
                
                wrap([$class: 'BuildUser']) {
                    script {
                        echo "触发用户ID: ${env.BUILD_USER_ID}"      // 如 'admin'
                        echo "触发用户名: ${env.BUILD_USER_NAME}"    // 如 'Admin User'
                        echo "触发用户邮箱: ${env.BUILD_USER_EMAIL}" // 如 'admin@example.com'
                    }
                }
                
                script {
                
                    //println("hello world")
                    //println(currentBuild.displayName)
                    //println(currentBuild)
                    
                    // 定义日期时间格式：年-月-日 时:分:秒
                    def dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
                    def currentDateTime = dateFormat.format(new Date())
                    //println(currentBuild.displayName)
                    //println("$currentDateTime")
                    def description = currentBuild.displayName + "\n" + "$currentDateTime"
                    //currentBuild.displayName = displayName
                    currentBuild.description = "时间: $currentDateTime" + "\n" + "分支: xx" + "\n" + "环境: xx"

                    print("${env.CHANGE_AUTHOR}")
                    print("${env.CHANGE_AUTHOR_DISPLAY_NAME}")
                    print("${env.CHANGE_AUTHOR_EMAIL}")
                    
                }
            }
        }

        stage('检出代码/ checkout code') {
            steps {
                echo '检出代码'
                
                script {
                
                    println("checkout code")
                    
                }
            }
        }
        
        
    }
}
