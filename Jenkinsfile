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
        sh "mv ../workdir_home/node_modules ../node 2>/dev/null"
        sh "rm -fr ../workdir_home/* ../workdir_home/.* 2>/dev/null"
        sh "mv ../node/node_modules ../workdir_home"
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
