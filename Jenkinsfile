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
                            echo('DRY_RUN = TRUE : ...')
                        } else {
                            echo('DRY_RUN = FALSE : ...')
                        }
                    }
                    catch (e) {
                        echo('detected failure: function_PSTA_ISCALA_36()')
                        throw(e)
                    }
                }
            }
        }
    }
}