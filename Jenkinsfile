node {

    stage('scm'){
        checkout scm
    }

    stage('git'){

        sh "branchname=`git branch -a | grep remotes/origin/PR`"
        sh "git checkout \$branchname"
    }
    
    stage('mv'){
        sh "mkdir -p ../workdir_home"
        sh "rm -rf `find ../workdir_home/* -not -name 'node_modules/*'`"
        sh "mv * .[^\\.]* ../workdir_home"
    }
    
    stage('build'){
        dir("/var/lib/jenkins/workspace/workdir_home"){
        sh "npm install"
        sh "ng test --varbose >tmp"
        sh "if [ `wc -l tmp |awk '{ print \$1 }'` -gt 0 ] ; then cat SIPPAI; else echo SEIKOU ; fi"
        }
    }
}
