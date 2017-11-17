node() {
stage("Clone"){
    git url: 'https://github.com/marionschlotte/shinecf.git'
}

stage("Build"){
 sh "java -jar /opt/sap/mta.jar --build-target=CF --mtar=shine_cf.mtar build"
    
}
stage("Deploy"){
    withCredentials([usernamePassword(credentialsId: 'Demo123', passwordVariable: 'CF_PASSWD', usernameVariable: 'CF_USER')]) {
        sh "cf api https://api.cf.eu10.hana.ondemand.com"
        sh "cf login -u $CF_USER -p $CF_PASSWD"
        sh "cf deploy shine_cf.mtar"
        sh "cf apps"
    }

}
}
