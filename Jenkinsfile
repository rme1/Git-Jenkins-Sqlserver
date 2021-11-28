pipeline{
    agent any
    options{
        timestamps()
    }
    parameters{
        password(name: "TEST_PASSWORD", defaultValue: "Budget#2021", description: "Sample password parameter")
        booleanParam(name: 'DRY_RUN', defaultValue: false, description: 'Just run Pipeline without execution ...')
        string(name: 'SQLSTATEMENT', defaultValue: 'EXEC [dbo].[sp_AddPerson]', description: 'dieses Statement soll ausgeführt werden ...')
    }
    stages{
        stage('SqlServerExecuteCommand'){
            steps{
                script{
                    try {
                        if (params.DRY_RUN == true) {
                            echo('fnExecuteSql(Ralf Merznicht)')
                        } else {
                            fnExecuteSql()
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
    stage('Execute SQL Statment'){
        script{
            powershell script:
              '''
              Write-Output "----------------------------------------------------------------"
              $SqlStatement = ${env:SQLSTATEMENT}
              Write-Output "SqlStatement --> $SqlStatement"
              Write-Output "----------------------------------------------------------------"
              $Datenquelle = "localhost,1433"
              $Benutzer = "sa"
              $Passwort = "Budget#2021"
              $Datenbank = "merzi"
              Invoke-Sqlcmd -Query $SqlStatement -ServerInstance $Datenquelle -database $Datenbank -QueryTimeout 65535 -ErrorAction 'Stop' -username $Benutzer -password $Passwort
              '''
        }
    }
}