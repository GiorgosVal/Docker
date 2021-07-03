FROM drupal:9

# Installs git in the drupal container
# the 'rm -rf /var/lib/apt/lists/*' performs a cleanup after apt-get update
RUN apt-get update \ 
    && apt-get install -y git \ 
    && rm -rf /var/lib/apt/lists/*

# Change the working dir so as to use it it the git clone
WORKDIR /var/www/html/themes

# Clones the drupal bootstrap theme. Specificaly, clones:
#   from the repo       https://git.drupal.org/project/bootstrap.git
#   the --branch        8.x-4.x
#   --signle-branch     Clones only the history leading to the tip of the branch
#   --depth 1           Shallow clone with the history truncated to last commit
# The above git clone command saves time and space, as it clones only the
# specific branch and commit we need, and not the while repo/branch history
#
# After the clone we change the ownership of the cloned directory
RUN git clone --branch 8.x-4.x --single-branch --depth 1 https://git.drupal.org/project/bootstrap.git \
    && chown -R www-data:www-data bootstrap

WORKDIR /var/www/html