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
        sh "mkdir -p ../node"
        sh "mkdir -p ../workdir_home/node_modules"
        sh "mv ../workdir_home/node_modules ../node 2>/dev/null"
        sh "rm -fr ../workdir_home/* ../workdir_home/.* | echo skip"
        sh "mv ../node/node_modules ../workdir_home"
        sh "mv * .[^\\.]* ../workdir_home"
    }
    
    stage('build'){
        dir("/var/lib/jenkins/workspace/workdir_home"){
        sh "npm install"
        sh "xvfb-run ng e2e ; echo \$? > tmp | echo skip"
        sh "if `cat tmp | grep 1` ; then cat SIPPAI; else echo SEIKOU ; fi"
        }
    }
}
