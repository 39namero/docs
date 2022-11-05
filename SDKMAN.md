# SDKMAN （java は SDKMAN！）

SDKMAN
https://sdkman.io/install

curl -s "https://get.sdkman.io" | bash

sdk version
S

sdk list java
    S
    Semeru        |     | 18.0.1.1     | sem     |            | 18.0.1.1-sem        
                |     | 17.0.3       | sem     |            | 17.0.3-sem          
                |     | 11.0.15      | sem     |            | 11.0.15-sem         
                |     | 8.0.332      | sem     |            | 8.0.332-sem         
    Temurin       |     | 18.0.1       | tem     |            | 18.0.1-tem          
                |     | 17.0.3       | tem     |            | 17.0.3-tem          
                |     | 11.0.15      | tem     |            | 11.0.15-tem         
                |     | 8.0.332      | tem     |            | 8.0.332-tem     
    S
sdk install java 8.0.332-sem

    Downloading: java 8.0.332-sem

    In progress...

    ################################################################################################################################################## 100.0%

    Repackaging Java 8.0.332-sem...

    Done repackaging...

    Installing: java 8.0.332-sem
    Done installing!


    Setting java 8.0.332-sem as default.

sdk current java

    Using java version 8.0.332-sem


sdk install java 8.0.332-tem

    Downloading: java 8.0.332-tem

    In progress...

    ################################################################################################################################################## 100.0%

    Repackaging Java 8.0.332-tem...

    Done repackaging...

    Installing: java 8.0.332-tem
    Done installing!

    Do you want java 8.0.332-tem to be set as default? (Y/n): y

    Setting java 8.0.332-tem as default.


vi .zshrc
```
〜
# 2022.6.1 add homebrew
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="$HOME/.sdkman"
[[ -s "$HOME/.sdkman/bin/sdkman-init.sh" ]] && source "$HOME/.sdkman/bin/sdkman-init.sh"

# 2022.6.21 add anyenv
export PATH="$HOME/.anyenv/bin:$PATH"
# 2022.6.1 add anyenv
eval "$(anyenv init -)"
```

jenv global temurin64-1.8.0.332

jenv versions 
    system
    1.8
    1.8.0.312
    1.8.0.332
    11
    11.0
    11.0.15
    17
    17.0
    17.0.3
    openjdk64-1.8.0.312
    openjdk64-11.0.15
    openjdk64-17.0.3
    semeru64-1.8.0.332
    * temurin64-1.8.0.332 (set by /home/ichiro/.anyenv/envs/jenv/version)


sdk install java 11.0.15-sem

sdk install java 11.0.15-tem

jenv add /home/ichiro/.sdkman/candidates/java/11.0.15-sem

jenv add /home/ichiro/.sdkman/candidates/java/11.0.15-tem


sdk install java 17.0.3-sem

sdk install java 17.0.3-tem

jenv add /home/ichiro/.sdkman/candidates/java/17.0.3-sem

jenv add /home/ichiro/.sdkman/candidates/java/17.0.3-tem


