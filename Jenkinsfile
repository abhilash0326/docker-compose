pipeline{
			agent{
				label{
					label 'slave-1'
					customWorkspace '/mnt'
				}
			}
		stages{
				
				stage ('installing git'){
										dir ('/mnt/projects'){
										steps{
												sh "rm -rf *"
												sh "yum install git -y"
												sh "git clone https://github.com/abhilash0326/game-of-life.git"
											}
										}
				}
				stage ('installing maven'){
										dir ('/mnt/projects/game-of-life'){
										steps{
												sh "rm -rf /root/.m2/repository"
												sh "mvn clean install"
											}
										}
				}
				stage ('transfering file from target'){
										dir ('/mnt/docker'){
										steps{
												
												sh "yum install docker -y"
												sh "systemctl start docker"
												sh "rm -rf gameoflife.war"
												sh "cp /mnt/projects/game-of-life/gameoflife-web/target/gameoflife.war ."
											}
										}
				}
				
				stage ('deployment of game of life'){
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
