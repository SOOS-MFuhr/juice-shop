pipeline {
    agent any

    environment {
        SOOS_PROJECT_NAME = "SOOS_DAST_Analysis_Jenkins_Test"
        SOOS_SCAN_MODE = "baseline"
        SOOS_API_BASE_URL= "https://dev-api.soos.io/api/"
        SOOS_TARGET_URL= "https://soos-dast-juice-shop.herokuapp.com/"
    }

    stages {
        stage('SOOS DAST Analysis') {
            steps {
                sh '''
                    PARAMS="--clientId=${SOOS_CLIENT_ID} --apiKey=${SOOS_API_KEY} --projectName=${SOOS_PROJECT_NAME} --scanMode=${SOOS_SCAN_MODE} --apiURL=${SOOS_API_BASE_URL}"
                    
                    if ( ${SOOS_DEBUG} == "true" ) then
                        PARAMS="${PARAMS} --debug=true"
                    fi
                    if ( ${SOOS_AJAX_SPIDER} == "true" ) then
                        PARAMS="${PARAMS} --ajaxSpider=true"
                    fi
                    if [ ! -z ${SOOS_RULES} ]; then
                        PARAMS="${PARAMS} --rules=\"$SOOS_RULES\""
                    fi
                    if [ ! -z ${SOOS_CONTEXT_FILE} ]; then
                        PARAMS="${PARAMS} --contextFile=${SOOS_CONTEXT_FILE}"
                    fi
                    if [ ! -z ${SOOS_CONTEXT_USER} ]; then
                        PARAMS="${PARAMS} --contextUser=${SOOS_CONTEXT_USER}"
                    fi
                    if [ ! -z ${SOOS_FULL_SCAN_MINUTES} ]; then
                        PARAMS="${PARAMS} --fullScanMinutes=${SOOS_FULL_SCAN_MINUTES}"
                    fi
                    if [ ! -z ${SOOS_API_SCAN_FORMAT} ]; then
                        PARAMS="${PARAMS} --apiScanFormat=${SOOS_API_SCAN_FORMAT}"
                    fi
                    if [ ! -z ${SOOS_LEVEL} ]; then
                        PARAMS="${PARAMS} --level=${SOOS_LEVEL}"
                    fi
   
                    docker run --rm soosio/dast:alpha ${SOOS_TARGET_URL} $PARAMS
                '''
            }
        }
    }
}