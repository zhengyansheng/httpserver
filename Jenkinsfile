
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                
                script {
                
                    println("hello world")
                    println(currentBuild.displayName)
                    println(currentBuild)
                    
                    // 定义日期时间格式：年-月-日 时:分:秒
                    def dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
                    def currentDateTime = dateFormat.format(new Date())
                    println(currentBuild.displayName)
                    println("$currentDateTime")
                    def displayName = currentBuild.displayName + "\n" + "$currentDateTime"
                    currentBuild.displayName = displayName
                    
                }
            }
        }
    }
}
