pipeline{
    agent any
    options{
        timestamps()
    }
    parameters{
        booleanParam(name: 'DRY_RUN', defaultValue: true, description: 'Just run Pipeline without execution ...')
    }
    stages{
        stage('SqlServerExecuteCommand'){
            steps{
                script{
                    try {
                        if (params.DRY_RUN == true) {
                            echo('fnExecuteSql(Ralf Merznicht)')
                        } else {
                            fnExecuteSql('Ralf Merznicht')
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

def fnExecuteSql(pStatementToExecute){
    powershell script: '''
        Write-Output "------> $(pStatementToExecute)"
    '''
}