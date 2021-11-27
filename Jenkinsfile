pipeline{
    agent any
    options{
        timestamps()
    }
    parameters{
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
    powershell script: '''
        Write-Output "----------------------------------------------------------------"
        $SqlStatement = ${env:SQLSTATEMENT}
        $Datenquelle = 'localhost,1433'
        $Benutzer = "sa"
        $Passwort = "Budget#2021"
        $Datenbank = "merzi"
        Invoke-Sqlcmd -ServerInstance $Datenquelle -Database $Datenbank -Username $Benutzer -Password $Passwort -Query "$SqlStatement"
        Write-Output "----------------------------------------------------------------"
    '''
}