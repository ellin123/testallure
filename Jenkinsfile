pipeline{
    agent any // 设置Jenkins调用节点，any表示master和slave都可
    stages{ // 里面可以填充多个stage
        
        stage('testallure') {
            steps{bat '''pytest test --alluredir ./report/allure_raw
'''
                
            }
        }
//         stage('testSetProperty'){
//             steps{
               
//                 sh '(python -m pytest test -s -q --alluredir ${WORKSPACE}/report/allure-results)' 
//                   // sh相当于开辟一个执行进程，当执行脚本是有多个步骤时，需要写到一起；pipeline执行完成之后回收进程，这时默认的根目录是job的工作目录，下个stage执行命令时需要注意
//             }
//         }
      }
    post('Results') { // 执行之后的操作
        always{
            script{// 集成allure，目录需要和保存的results保持一致，注意此处目录为job工作目录之后的目录，Jenkins会自动将根目录与path进行拼接
                allure includeProperties: false, jdk: '', report: 'report/allure-report', results: [[path: 'report/allure-results']]
            }
            }
    }
}
