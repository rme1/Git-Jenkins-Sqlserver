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
            psta_iscala_36.LoadTables()
        }
    }
}