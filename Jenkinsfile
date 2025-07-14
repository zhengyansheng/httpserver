
pipeline {
    agent any

    stages {
        stage('初始化/ initialization') {
            steps {
                echo '初始化'
                
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
