// commit muss ankommen
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
                            echo "psta_iscala_36.LoadTables()"
                            ExecuteSql('aasdf','asdf','asdf')
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

def ExecuteSql(String pSchema, String pProcedureName, String pBuildId){
    //withCredentials([usernamePassword(credentialsId: 'rm1', usernameVariable: 'USER_ID', passwordVariable: 'USER_PASSWORD')])
    //{
        withEnv(["InFunctSchema=${pSchema}","InFunctProcedureName=${pProcedureName}","InFunctBuildId=${pBuildId}"])
        {
            powershell encoding: 'UTF-8', CodePage: 1252, script:
                '''
                $pw = "gmcsTtmE80N6GN§DFdvvurn§"
                Write-Output "----------------------------------------------------------------"
                Write-Output "----------------------------------------------------------------"                
                $OutputEncoding
                Write-Output "----------------------------------------------------------------"                                
                Write-Output "pw --> $pw"
                Write-Output "----------------------------------------------------------------"                

                $InShellSchema = ${env:InFunctSchema}
                $InShellProcedureName = ${env:InFunctProcedureName}
                $InShelltBuildId = ${env:InFunctBuildId}
               
                $InShellServer = 'zde01sql9291'
                Write-Output "----------------------------------------------------------------"
                Write-Output "InShellServer --> $InShellServer"
                Write-Output "----------------------------------------------------------------"
 
                $InShellUser = ${env:USER_ID}
                Write-Output "----------------------------------------------------------------"
                Write-Output "InShellUser --> $InShellUser"
                Write-Output "----------------------------------------------------------------"
 
                # $InShellPassword = ${env:USER_PASSWORD}
 
                $StatementToExecuteComplete = 'EXEC [' + $InShellSchema + '].[' + $InShellProcedureName + '] ' + $InShelltBuildId
                $StatementGetInfo = 'SELECT * FROM META.t_LoggingSql WHERE [Procedure] = TRIM('' ' + $InShellProcedureName + ' '') AND ExecutionId = ' + $InShelltBuildId
                Write-Output "----------------------------------------------------------------"              
                Write-Output "----------------------------------------------------------------"
                Write-Output "StatementToExecuteComplete --> $StatementToExecuteComplete"
                Write-Output "----------------------------------------------------------------"              
                Write-Output "StatementGetInfo --> $StatementGetInfo"
                Write-Output "----------------------------------------------------------------"              
                Write-Output "----------------------------------------------------------------"              
                $Datenbank = "JHDWH"
                # Invoke-Sqlcmd -Query $StatementToExecuteComplete -ServerInstance $InShellServer -database $Datenbank -QueryTimeout 65535 -ErrorAction 'Stop' -username $InShellUser -password $env:USER_PASSWORD
                # $GetInfo = Invoke-Sqlcmd -Query $StatementGetInfo -ServerInstance $InShellServer -database $Datenbank -QueryTimeout 65535 -ErrorAction 'Stop' -username $InShellUser -password $env:USER_PASSWORD
                # write-host ($GetInfo | Format-Table | Out-String)
                '''
        }
    //}
}