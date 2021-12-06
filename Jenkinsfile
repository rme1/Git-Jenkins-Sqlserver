@Library('libs') _

pipeline{
    agent any
    options{
        timestamps()
    }
    parameters{
        password(name: "PASSWORD", defaultValue: "Budget#2021", description: "Sample password parameter")
        booleanParam(name: 'DRY_RUN', defaultValue: false, description: 'Just run Pipeline without execution ...')
        string(name: 'SQLSTATEMENT', defaultValue: "EXEC [dbo].[sp_AddPerson] 99,'Ralf Merznicht'", description: "dieses Statement soll ausgeführt werden ...")
    }
    stages{
        stage('SqlServerExecuteCommand'){
            steps{
                script{
                    try {
                        if (params.DRY_RUN == true) {
                            echo('fnExecuteSql(${env:SQLSTATEMENT})')
                        } else {
                            //psfunctions.fnExecuteSql("${env:SQLSTATEMENT}")
                            psta_iscala_36.LoadTables()
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