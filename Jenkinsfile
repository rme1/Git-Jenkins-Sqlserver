pipeline{
    agent any
    options{
        timestamps()
    }
    parameters{
        password(name: "PASSWORD", defaultValue: "Budget#2021", description: "Sample password parameter")
        booleanParam(name: 'DRY_RUN', defaultValue: false, description: 'Just run Pipeline without execution ...')
        string(name: 'SQLSTATEMENT', defaultValue: "EXEC [dbo].[sp_AddPerson]", description: "dieses Statement soll ausgeführt werden ...")
        string(name: 'SQLSTATEMENT_GETINFO', defaultValue: "SELECT TOP (1000) [Title],[FirstName],[MiddleName],[LastName] FROM [merzi].[dbo].[Person] WHERE Title = 'X'", description: "nachsehen was passiert ist ...")
    }
    stages{
        stage('SqlServerExecuteCommand'){
            steps{
                script{
                    try {
                        if (params.DRY_RUN == true) {
                            echo('fnExecuteSql(Ralf Merznicht)')
                        } else {
                            fnExecuteSql('ASDF')
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


def fnExecuteSql(pUebergabe){
    steps{
        echo('ASDF')
    }
}

/*
def fnExecuteSql(pUebergabe){
    stage('Execute SQL Statment'){
        script{
            echo('asdf : ${pUebergabe}')
            echo('${JOB_URL}')
            powershell script:
              '''
              Write-Output "----------------------------------------------------------------"              
              Write-Output "----------------------------------------------------------------"
              $SqlStatement = ${env:SQLSTATEMENT}
              Write-Output "SqlStatement --> $SqlStatement"
              Write-Output "----------------------------------------------------------------"              
              $SqlStatementGetInfo = ${env:SQLSTATEMENT_GETINFO}
              Write-Output "SqlStatementGetInfo --> $SqlStatementGetInfo"              
              Write-Output "----------------------------------------------------------------"
              Write-Output "----------------------------------------------------------------"              
              $Datenquelle = "localhost,1433"
              $Datenbank = "merzi"
              $Benutzer = "sa"
              $Passwort = ${env:PASSWORD}
              Invoke-Sqlcmd -Query $SqlStatement -ServerInstance $Datenquelle -database $Datenbank -QueryTimeout 65535 -ErrorAction 'Stop' -username $Benutzer -password $Passwort
              $GetInfo = Invoke-Sqlcmd -Query $SqlStatementGetInfo -ServerInstance $Datenquelle -database $Datenbank -QueryTimeout 65535 -ErrorAction 'Stop' -username $Benutzer -password $Passwort
              write-host ($GetInfo | Format-Table | Out-String) 
              '''
        }
    }
}
*/