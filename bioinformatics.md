/NGS/Nextseq/190808_NB552054_0001_AHC2KFBGXB/
/NGS/Nextseq/190901_NB552054_0006_AHC35WBGXB

$ sudo docker run -t \
    -v /etc/localtime:/etc/localtime \
    -v /NGS/Nextseq/190808_NB552054_0001_AHC2KFBGXB:/data \
    -v /tmp/resources:/genomes \
    -v /tmp/analysis:/analysis \
    docker-oncology.dockerhub.illumina.com/zodiac/tst170localapp:2.0.0.39