pipeline{
    agent any
    options{
        timestamps()
    }
    parameters{
        booleanParam(name: 'DRY_RUN', defaultValue: true, description: 'Just run Pipeline without execution ...')
        string(name: 'SQLSTATEMENT', defaultValue: 'SELECT ''Ralf Merznicht''', description: 'dieses Statement soll ausgeführt werden ...')
    }
    stages{
        stage('SqlServerExecuteCommand'){
            steps{
                script{
                    try {
                        if (params.DRY_RUN == true) {
                            echo('fnExecuteSql(Ralf Merznicht)')
                        } else {
                            fnExecuteSql(env:SQLSTATEMENT)
                        }
                    }
                    catch (e) {
                        echo('detected failure ... --> TODO Get Failure !!!')
                        throw(e)
                    }
                }
            }
        }
    }
}

def fnExecuteSql(){
    powershell script: '''
        Write-Output "----------------------------------------------------------------"
        $SqlStatement = ${env:SQLSTATEMENT}
        Write-Output "----> SqlStatement: $SqlStatement"
        Write-Output "----------------------------------------------------------------"
    '''
}