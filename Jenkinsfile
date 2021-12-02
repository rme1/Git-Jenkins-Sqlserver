@Library('lib') _

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
                            lib.fnExecuteSql("${env:SQLSTATEMENT}")
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

/*
def fnExecuteSql(String pStatementToExecute){
    withEnv(["InFunctStatementToExecute=${pStatementToExecute}"])
    {
        powershell script:
              '''
              $InShellStatementToExecute = ${env:InFunctStatementToExecute}
              Write-Output "----------------------------------------------------------------"              
              Write-Output "----------------------------------------------------------------"
              Write-Output "SqlStatement --> $InShellStatementToExecute"
              Write-Output "----------------------------------------------------------------"              
              Write-Output "----------------------------------------------------------------"              
              $Datenquelle = "localhost,1433"
              $Datenbank = "merzi"
              $Benutzer = "sa"
              $Passwort = ${env:PASSWORD}
              Invoke-Sqlcmd -Query $InShellStatementToExecute -ServerInstance $Datenquelle -database $Datenbank -QueryTimeout 65535 -ErrorAction 'Stop' -username $Benutzer -password $Passwort
              write-host ($GetInfo | Format-Table | Out-String) 
              '''
    }       
}
*/
