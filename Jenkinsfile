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
    stage('Execute SQL Statment'){
        script{
            //try{
                env.MY_RESULT = powershell(returnStdout: true, script:
                  '''
                  get-host
                  Write-Output "----------------------------------------------------------------"
                  $SqlStatement = ${env:SQLSTATEMENT}
                  Write-Output "SqlStatement --> $SqlStatement"
                  Write-Output "----------------------------------------------------------------"
                  $Datenquelle = "localhost,1433"
                  $Benutzer = "sa"
                  $Passwort = "Budget#2021"
                  $Datenbank = "merzi"
                  try{
                     Invoke-Sqlcmd -ServerInstance $Datenquelle -Database $Datenbank -Username $Benutzer -Password $Passwort -Query "$SqlStatement"
                  } catch {
                      "error when running $SqlStatement"
                      Write-Error 'The file does not exist' -ErrorAction Stop
                  }
                  ''')
            //} catch(err){
            //    echo err.getMessage()
            //}
            echo "${env.MY_RESULT}"
        }
    }
}

//        try{

//        }
//        catch{
//            exit $LastExitCode
//        }