//Pipeline declarativo
pipeline {
    
    // Ejecutar el pipeline desde un agente concreto
  agent {
    node{
      label 'principal' 
    }
  }
    
    // Opciones pipeline
    options {
      // FIcheros de Log
      buildDiscarder logRotator(
        daysToKeepStr: '15',
        numToKeepStr: '10'
      )        
    }
    
    // Definicion de Fases
    stages {
        
        stage('Cleanup Workspace') {
            
            //Conjuntos de pasos que componen la fase
            steps {
              cleanWs()
              echo 'Eliminado Workspace para Job';                
            }            
        }
      
        stage('Code Checkout') {
            
            //Conjuntos de pasos que componen la fase
            steps {
              checkout(
                $class: 'GitSCM',
                branches: [[name: '*/main']],
                userRemoteConfigs: [[url: 'https://github.com/spring-projects/sprin-petclinic.git']]
              )               
            }            
        }
      
      stage('Unit Testing') {
        when {
            branch 'testing' 
         }
            
            //Conjuntos de pasos que componen la fase
            steps {
              echo 'Runing Unit Tests';                            
            }            
       }
      
      stage('Code Analysis') {
            
            //Conjuntos de pasos que componen la fase
            steps {
              echo 'Runing Code Analysis';                            
            }            
       }
      
       stage('Build Deploy Code') {
         
         when {
            branch 'developer' 
         }
            
            //Conjuntos de pasos que componen la fase
            steps {
              echo 'Building Artifact';
              
              echo 'Deploying Code';   
            }            
       }
      
    } 
    
    
}
