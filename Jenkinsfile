pipeline{
			agent{
				label{
					label 'slave-1'
					customWorkspace '/mnt/projects'
				}
			}
		stages{
				
				stage ('installing git'){
										steps{
												sh "rm -rf *"
												sh "yum install git -y"
												sh "git clone https://github.com/abhilash0326/game-of-life.git"
											}
				}
				stage ('building .war file'){
										steps {
												dir ('/mnt/projects/game-of-life/'){
													sh "rm -rf /root/.m2/"
													sh "rm -rf /mnt/projects/game-of-life/gameoflife-web/target"
													sh "mvn install"
													
												}
										}
					
					}
				stage ('transfering file from target'){
					steps{					
										dir ('/mnt/docker/'){
										steps{
												
												sh "sudo yum install docker -y"
												sh "sudo systemctl start docker"
												sh "sudo rm -rf gameoflife.war"
												sh "cp /mnt/projects/game-of-life/gameoflife-web/target/gameoflife.war ."
											}
										}
					}
				}
				
				stage ('deployment of game of life'){
					steps{
										dir ('/mnt'){
										steps{
												sh "curl -SL https://github.com/docker/compose/releases/download/v2.11.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose"
												sh "sudo chmod +x /usr/local/bin/docker-compose"
												sh "sudo chmod +x /usr/bin/docker-compose"
												sh "docker-compose down"
												sh "docker-compose up -d"
											}
										}
					}
				}
		}
}
