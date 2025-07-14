
// setBuildDisplayName 设置构建显示的名称
def setBuildDisplayName() {
    // 定义日期时间格式：年-月-日 时:分:秒
    def dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
    def currentDateTime = dateFormat.format(new Date())
    def description = currentBuild.displayName + "\n" + "$currentDateTime"
    currentBuild.description = "时间: $currentDateTime" + "\n" + "分支: xx" + "\n" + "环境: xx" + "\n" + "用户: ${env.EXECUTE_JOB_USER_ID}"
}

def checkoutCode() {

}



// 流水线
pipeline {

    // 执行的节点
    agent any

    // 阶段
    stages {
        stage('初始化/ initialization') {
            steps {
                echo '初始化'
                
                wrap([$class: 'BuildUser']) {
                    script {
                        echo "触发用户ID: ${env.BUILD_USER_ID}"      // 如 'admin'
                        env.EXECUTE_JOB_USER_ID = "${env.BUILD_USER_ID}"
                    }
                }
                
                script {

                    setBuildDisplayName()

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

        stage('编译/ build') {
            steps {
                echo '编译'

                script {

                    println("build")

                }
            }
        }

        stage('构建和推送镜像/ build and push image') {
            steps {
                echo '构建和推送镜像'

                script {

                    println("build and push image")

                }
            }
        }
        
        stage('部署/ deployment') {
            steps {
                echo '部署'

                script {

                    println("deployment")

                }
            }
        }

    }

    // 钩子
    post {
      always {
            script {
                println("job执行结束")
            }
      }
      aborted {
            script {
                println("job终止")
            }
      }
      success {
            script {
                println("job执行成功")
            }
      }
      failure {
            script {
                println("job执行失败")
            }
      }
    }


}
