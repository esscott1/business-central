
# This is a Dockerfile for the rhpam-7/rhpam-businesscentral-rhel8:7.11.0 image.


## START target image rhpam-7/rhpam-businesscentral-rhel8:7.11.0
## \
    FROM registry.redhat.io/ubi8/ubi-minimal:latest


    USER root

###### START module 'jboss.kie.common.dependencies:1.0'
###### \
        # Switch to 'root' user to install 'jboss.kie.common.dependencies' module defined packages
        USER root
        # Install packages defined in the 'jboss.kie.common.dependencies' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y findutils hostname \
            && microdnf clean all \
            && rpm -q findutils hostname
###### /
###### END module 'jboss.kie.common.dependencies:1.0'

###### START module 'jboss.container.user:1.0'
###### \
        # Copy 'jboss.container.user' module content
        COPY modules/jboss.container.user /tmp/scripts/jboss.container.user
        # Switch to 'root' user to install 'jboss.container.user' module defined packages
        USER root
        # Install packages defined in the 'jboss.container.user' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y unzip tar rsync shadow-utils \
            && microdnf clean all \
            && rpm -q unzip tar rsync shadow-utils
        # Set 'jboss.container.user' module defined environment variables
        ENV \
            HOME="/home/jboss" 
        # Custom scripts from 'jboss.container.user' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.user/configure.sh" ]
###### /
###### END module 'jboss.container.user:1.0'

###### START module 'jboss.container.openjdk.jdk:11'
###### \
        # Copy 'jboss.container.openjdk.jdk' module content
        COPY modules/jboss.container.openjdk.jdk /tmp/scripts/jboss.container.openjdk.jdk
        # Switch to 'root' user to install 'jboss.container.openjdk.jdk' module defined packages
        USER root
        # Install packages defined in the 'jboss.container.openjdk.jdk' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y java-11-openjdk-devel \
            && microdnf clean all \
            && rpm -q java-11-openjdk-devel
        # Set 'jboss.container.openjdk.jdk' module defined environment variables
        ENV \
            JAVA_HOME="/usr/lib/jvm/java-11" \
            JAVA_VENDOR="openjdk" \
            JAVA_VERSION="11.0" \
            JBOSS_CONTAINER_OPENJDK_JDK_MODULE="/opt/jboss/container/openjdk/jdk" 
        # Set 'jboss.container.openjdk.jdk' module defined labels
        LABEL \
            org.jboss.product="openjdk"  \
            org.jboss.product.openjdk.version="11.0"  \
            org.jboss.product.version="11.0" 
        # Custom scripts from 'jboss.container.openjdk.jdk' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.openjdk.jdk/configure.sh" ]
###### /
###### END module 'jboss.container.openjdk.jdk:11'

###### START module 'jboss.container.java.jvm.api:1.0'
###### \
###### /
###### END module 'jboss.container.java.jvm.api:1.0'

###### START module 'jboss.container.proxy.api:2.0'
###### \
###### /
###### END module 'jboss.container.proxy.api:2.0'

###### START module 'jboss.container.java.proxy.bash:2.0'
###### \
        # Copy 'jboss.container.java.proxy.bash' module content
        COPY modules/jboss.container.java.proxy.bash /tmp/scripts/jboss.container.java.proxy.bash
        # Set 'jboss.container.java.proxy.bash' module defined environment variables
        ENV \
            JBOSS_CONTAINER_JAVA_PROXY_MODULE="/opt/jboss/container/java/proxy" 
        # Custom scripts from 'jboss.container.java.proxy.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.java.proxy.bash/configure.sh" ]
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.java.proxy.bash/backward_compatibility.sh" ]
###### /
###### END module 'jboss.container.java.proxy.bash:2.0'

###### START module 'jboss.container.java.jvm.bash:1.0'
###### \
        # Copy 'jboss.container.java.jvm.bash' module content
        COPY modules/jboss.container.java.jvm.bash /tmp/scripts/jboss.container.java.jvm.bash
        # Set 'jboss.container.java.jvm.bash' module defined environment variables
        ENV \
            JBOSS_CONTAINER_JAVA_JVM_MODULE="/opt/jboss/container/java/jvm" 
        # Custom scripts from 'jboss.container.java.jvm.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.java.jvm.bash/configure.sh" ]
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.java.jvm.bash/backward_compatibility.sh" ]
###### /
###### END module 'jboss.container.java.jvm.bash:1.0'

###### START module 'dynamic-resources:1.0'
###### \
        # Copy 'dynamic-resources' module content
        COPY modules/dynamic-resources /tmp/scripts/dynamic-resources
        # Custom scripts from 'dynamic-resources' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/dynamic-resources/install.sh" ]
###### /
###### END module 'dynamic-resources:1.0'

###### START module 'eap-73-env:7.3.6'
###### \
        # Set 'eap-73-env' module defined environment variables
        ENV \
            JBOSS_EAP_VERSION="7.3.6" \
            JBOSS_HOME="/opt/eap" \
            JBOSS_PRODUCT="eap" \
            LAUNCH_JBOSS_IN_BACKGROUND="true" \
            PRODUCT_VERSION="7.3.6" \
            WILDFLY_VERSION="7.3.6.GA-redhat-00002" 
        # Set 'eap-73-env' module defined labels
        LABEL \
            com.redhat.deployments-dir="/opt/eap/standalone/deployments"  \
            com.redhat.dev-mode="DEBUG:true"  \
            com.redhat.dev-mode.port="DEBUG_PORT:8787"  \
            org.jboss.product="eap"  \
            org.jboss.product.eap.version="7.3.6"  \
            org.jboss.product.version="7.3.6" 
        # Exposed ports in 'eap-73-env' module
        EXPOSE 8080
###### /
###### END module 'eap-73-env:7.3.6'

###### START module 'eap-73-env-latest:1.0'
###### \
###### /
###### END module 'eap-73-env-latest:1.0'

###### START module 'eap-736:7.3.6'
###### \
        # Copy 'eap-736' module general artifacts to '/tmp/artifacts/' destination
        COPY \
            artifacts/jboss-eap-7.3.zip \
            jboss-eap-7.3.6-patch.zip \
            /tmp/artifacts/
        # Copy 'eap-736' module content
        COPY modules/eap-736 /tmp/scripts/eap-736
        # Custom scripts from 'eap-736' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/eap-736/install.sh" ]
###### /
###### END module 'eap-736:7.3.6'

###### START module 'eap-install-cleanup:1.0'
###### \
        # Copy 'eap-install-cleanup' module content
        COPY modules/eap-install-cleanup /tmp/scripts/eap-install-cleanup
        # Custom scripts from 'eap-install-cleanup' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/eap-install-cleanup/install.sh" ]
###### /
###### END module 'eap-install-cleanup:1.0'

###### START module 'eap-73-latest:7.3-latest'
###### \
###### /
###### END module 'eap-73-latest:7.3-latest'

###### START module 'jboss.container.eap.setup:1.0'
###### \
        # Copy 'jboss.container.eap.setup' module content
        COPY modules/jboss.container.eap.setup /tmp/scripts/jboss.container.eap.setup
        # Set 'jboss.container.eap.setup' module defined environment variables
        ENV \
            SSO_FORCE_LEGACY_SECURITY="true" 
        # Custom scripts from 'jboss.container.eap.setup' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.eap.setup/configure.sh" ]
###### /
###### END module 'jboss.container.eap.setup:1.0'

###### START module 'rhpam-7-businesscentral:1.0'
###### \
        # Copy 'rhpam-7-businesscentral' module general artifacts to '/tmp/artifacts/' destination
        COPY \
            artifacts/rhpam_business_central_distribution.zip \
            /tmp/artifacts/
        # Copy 'rhpam-7-businesscentral' module content
        COPY modules/rhpam-7-businesscentral /tmp/scripts/rhpam-7-businesscentral
        # Set 'rhpam-7-businesscentral' module defined environment variables
        ENV \
            BUSINESS_CENTRAL_DISTRIBUTION_EAP="jboss-eap-7.3" \
            BUSINESS_CENTRAL_DISTRIBUTION_ZIP="rhpam_business_central_distribution.zip" \
            JBOSS_PRODUCT="rhpam-businesscentral" \
            PRODUCT_VERSION="7.11.0" \
            RHPAM_BUSINESS_CENTRAL_VERSION="7.11.0" 
        # Set 'rhpam-7-businesscentral' module defined labels
        LABEL \
            org.jboss.product="rhpam-businesscentral"  \
            org.jboss.product.rhpam-businesscentral.version="7.11.0"  \
            org.jboss.product.version="7.11.0" 
        # Exposed ports in 'rhpam-7-businesscentral' module
        EXPOSE 8001
        # Custom scripts from 'rhpam-7-businesscentral' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/rhpam-7-businesscentral/install" ]
###### /
###### END module 'rhpam-7-businesscentral:1.0'

###### START module 'jboss.container.maven.module:3.6'
###### \
        # Copy 'jboss.container.maven.module' module content
        COPY modules/jboss.container.maven.module /tmp/scripts/jboss.container.maven.module
        # Custom scripts from 'jboss.container.maven.module' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.maven.module/configure.sh" ]
###### /
###### END module 'jboss.container.maven.module:3.6'

###### START module 'jboss.container.maven.36.bash:3.6'
###### \
        # Copy 'jboss.container.maven.36.bash' module content
        COPY modules/jboss.container.maven.36.bash /tmp/scripts/jboss.container.maven.36.bash
        # Switch to 'root' user to install 'jboss.container.maven.36.bash' module defined packages
        USER root
        # Install packages defined in the 'jboss.container.maven.36.bash' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y maven \
            && microdnf clean all \
            && rpm -q maven
        # Set 'jboss.container.maven.36.bash' module defined environment variables
        ENV \
            JBOSS_CONTAINER_MAVEN_36_MODULE="/opt/jboss/container/maven/36/" \
            MAVEN_VERSION="3.6" 
        # Set 'jboss.container.maven.36.bash' module defined labels
        LABEL \
            io.fabric8.s2i.version.maven="3.6" 
        # Custom scripts from 'jboss.container.maven.36.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.maven.36.bash/configure.sh" ]
###### /
###### END module 'jboss.container.maven.36.bash:3.6'

###### START module 'jboss.container.maven.api:1.0'
###### \
###### /
###### END module 'jboss.container.maven.api:1.0'

###### START module 'jboss.container.util.logging.bash:1.0'
###### \
        # Copy 'jboss.container.util.logging.bash' module content
        COPY modules/jboss.container.util.logging.bash /tmp/scripts/jboss.container.util.logging.bash
        # Set 'jboss.container.util.logging.bash' module defined environment variables
        ENV \
            JBOSS_CONTAINER_UTIL_LOGGING_MODULE="/opt/jboss/container/util/logging/" 
        # Custom scripts from 'jboss.container.util.logging.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.util.logging.bash/configure.sh" ]
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.util.logging.bash/backward_compatibility.sh" ]
###### /
###### END module 'jboss.container.util.logging.bash:1.0'

###### START module 'jboss.container.maven.default.bash:1.0'
###### \
        # Copy 'jboss.container.maven.default.bash' module content
        COPY modules/jboss.container.maven.default.bash /tmp/scripts/jboss.container.maven.default.bash
        # Set 'jboss.container.maven.default.bash' module defined environment variables
        ENV \
            JBOSS_CONTAINER_MAVEN_DEFAULT_MODULE="/opt/jboss/container/maven/default/" 
        # Custom scripts from 'jboss.container.maven.default.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.maven.default.bash/configure.sh" ]
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.maven.default.bash/backward_compatibility.sh" ]
###### /
###### END module 'jboss.container.maven.default.bash:1.0'

###### START module 'jboss.container.jolokia.api:1.0'
###### \
        # Set 'jboss.container.jolokia.api' module defined environment variables
        ENV \
            AB_JOLOKIA_AUTH_OPENSHIFT="true" \
            AB_JOLOKIA_HTTPS="true" \
            AB_JOLOKIA_PASSWORD_RANDOM="true" 
###### /
###### END module 'jboss.container.jolokia.api:1.0'

###### START module 'jboss.container.jolokia.bash:1.0'
###### \
        # Copy 'jboss.container.jolokia.bash' module general artifacts to '/tmp/artifacts/' destination
        COPY \
            artifacts/jolokia-jvm-1.6.2.redhat-00002-agent.jar \
            /tmp/artifacts/
        # Copy 'jboss.container.jolokia.bash' module content
        COPY modules/jboss.container.jolokia.bash /tmp/scripts/jboss.container.jolokia.bash
        # Set 'jboss.container.jolokia.bash' module defined environment variables
        ENV \
            AB_JOLOKIA_AUTH_OPENSHIFT="true" \
            AB_JOLOKIA_HTTPS="true" \
            AB_JOLOKIA_PASSWORD_RANDOM="true" \
            JBOSS_CONTAINER_JOLOKIA_MODULE="/opt/jboss/container/jolokia" \
            JOLOKIA_VERSION="1.6.2" 
        # Set 'jboss.container.jolokia.bash' module defined labels
        LABEL \
            io.fabric8.s2i.version.jolokia="1.6.2-redhat-00002" 
        # Exposed ports in 'jboss.container.jolokia.bash' module
        EXPOSE 8778
        # Custom scripts from 'jboss.container.jolokia.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.jolokia.bash/configure.sh" ]
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.jolokia.bash/backward_compatibility.sh" ]
###### /
###### END module 'jboss.container.jolokia.bash:1.0'

###### START module 'jboss.eap.cd.jolokia:1.0-kie'
###### \
        # Copy 'jboss.eap.cd.jolokia' module content
        COPY modules/jboss.eap.cd.jolokia /tmp/scripts/jboss.eap.cd.jolokia
        # Custom scripts from 'jboss.eap.cd.jolokia' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.eap.cd.jolokia/configure.sh" ]
###### /
###### END module 'jboss.eap.cd.jolokia:1.0-kie'

###### START module 'os-eap7-openshift:1.0-kie'
###### \
        # Copy 'os-eap7-openshift' module content
        COPY modules/os-eap7-openshift /tmp/scripts/os-eap7-openshift
        # Custom scripts from 'os-eap7-openshift' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/os-eap7-openshift/prepare.sh" ]
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/os-eap7-openshift/configure.sh" ]
###### /
###### END module 'os-eap7-openshift:1.0-kie'

###### START module 'jboss.eap.config.openshift:EAP7.3.0-kie'
###### \
        # Copy 'jboss.eap.config.openshift' module content
        COPY modules/jboss.eap.config.openshift /tmp/scripts/jboss.eap.config.openshift
        # Custom scripts from 'jboss.eap.config.openshift' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.eap.config.openshift/configure.sh" ]
###### /
###### END module 'jboss.eap.config.openshift:EAP7.3.0-kie'

###### START module 'os-eap-activemq-rar:1.1'
###### \
        # Copy 'os-eap-activemq-rar' module general artifacts to '/tmp/artifacts/' destination
        COPY \
            activemq-rar-5.11.0.redhat-630371.rar \
            /tmp/artifacts/
        # Copy 'os-eap-activemq-rar' module content
        COPY modules/os-eap-activemq-rar /tmp/scripts/os-eap-activemq-rar
        # Custom scripts from 'os-eap-activemq-rar' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/os-eap-activemq-rar/configure.sh" ]
###### /
###### END module 'os-eap-activemq-rar:1.1'

###### START module 'os-eap-launch:1.0-kie'
###### \
        # Copy 'os-eap-launch' module content
        COPY modules/os-eap-launch /tmp/scripts/os-eap-launch
        # Switch to 'root' user to install 'os-eap-launch' module defined packages
        USER root
        # Install packages defined in the 'os-eap-launch' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y hostname \
            && microdnf clean all \
            && rpm -q hostname
        # Set 'os-eap-launch' module defined environment variables
        ENV \
            DEFAULT_ADMIN_USERNAME="eapadmin" 
        # Custom scripts from 'os-eap-launch' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/os-eap-launch/configure.sh" ]
###### /
###### END module 'os-eap-launch:1.0-kie'

###### START module 'jboss.container.wildfly.launch.os.node-name:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.os.node-name' module content
        COPY modules/jboss.container.wildfly.launch.os.node-name /tmp/scripts/jboss.container.wildfly.launch.os.node-name
        # Custom scripts from 'jboss.container.wildfly.launch.os.node-name' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.os.node-name/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.os.node-name:1.0'

###### START module 'os-eap-migration:1.0'
###### \
        # Copy 'os-eap-migration' module content
        COPY modules/os-eap-migration /tmp/scripts/os-eap-migration
        # Custom scripts from 'os-eap-migration' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/os-eap-migration/configure.sh" ]
###### /
###### END module 'os-eap-migration:1.0'

###### START module 'os-eap7-launch:1.0-kie'
###### \
        # Copy 'os-eap7-launch' module content
        COPY modules/os-eap7-launch /tmp/scripts/os-eap7-launch
        # Set 'os-eap7-launch' module defined environment variables
        ENV \
            JBOSS_MODULES_SYSTEM_PKGS="org.jboss.logmanager,jdk.nashorn.api" 
        # Custom scripts from 'os-eap7-launch' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/os-eap7-launch/configure.sh" ]
###### /
###### END module 'os-eap7-launch:1.0-kie'

###### START module 'jboss-kie-db-drivers:1.0'
###### \
        # Copy 'jboss-kie-db-drivers' module content
        COPY modules/jboss-kie-db-drivers /tmp/scripts/jboss-kie-db-drivers
        # Switch to 'root' user to install 'jboss-kie-db-drivers' module defined packages
        USER root
        # Install packages defined in the 'jboss-kie-db-drivers' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y mariadb-java-client postgresql-jdbc \
            && microdnf clean all \
            && rpm -q mariadb-java-client postgresql-jdbc
        # Custom scripts from 'jboss-kie-db-drivers' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss-kie-db-drivers/configure.sh" ]
###### /
###### END module 'jboss-kie-db-drivers:1.0'

###### START module 'jboss.container.wildfly.launch.messaging:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.messaging' module content
        COPY modules/jboss.container.wildfly.launch.messaging /tmp/scripts/jboss.container.wildfly.launch.messaging
        # Custom scripts from 'jboss.container.wildfly.launch.messaging' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.messaging/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.messaging:1.0'

###### START module 'jboss.container.wildfly.launch.json-logging:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.json-logging' module content
        COPY modules/jboss.container.wildfly.launch.json-logging /tmp/scripts/jboss.container.wildfly.launch.json-logging
        # Custom scripts from 'jboss.container.wildfly.launch.json-logging' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.json-logging/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.json-logging:1.0'

###### START module 'jboss.container.wildfly.launch.mp-config:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.mp-config' module content
        COPY modules/jboss.container.wildfly.launch.mp-config /tmp/scripts/jboss.container.wildfly.launch.mp-config
        # Set 'jboss.container.wildfly.launch.mp-config' module defined environment variables
        ENV \
            MICROPROFILE_CONFIG_DIR_ORDINAL="500" 
        # Custom scripts from 'jboss.container.wildfly.launch.mp-config' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.mp-config/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.mp-config:1.0'

###### START module 'jboss.container.wildfly.launch-config.config:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch-config.config' module content
        COPY modules/jboss.container.wildfly.launch-config.config /tmp/scripts/jboss.container.wildfly.launch-config.config
        # Custom scripts from 'jboss.container.wildfly.launch-config.config' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch-config.config/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch-config.config:1.0'

###### START module 'jboss.container.wildfly.launch-config.os:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch-config.os' module content
        COPY modules/jboss.container.wildfly.launch-config.os /tmp/scripts/jboss.container.wildfly.launch-config.os
        # Set 'jboss.container.wildfly.launch-config.os' module defined environment variables
        ENV \
            JBOSS_MODULES_SYSTEM_PKGS="org.jboss.logmanager,jdk.nashorn.api,com.sun.crypto.provider" 
        # Custom scripts from 'jboss.container.wildfly.launch-config.os' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch-config.os/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch-config.os:1.0'

###### START module 'jboss.container.wildfly.launch.jgroups:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.jgroups' module content
        COPY modules/jboss.container.wildfly.launch.jgroups /tmp/scripts/jboss.container.wildfly.launch.jgroups
        # Custom scripts from 'jboss.container.wildfly.launch.jgroups' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.jgroups/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.jgroups:1.0'

###### START module 'jboss.container.wildfly.launch.elytron:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.elytron' module content
        COPY modules/jboss.container.wildfly.launch.elytron /tmp/scripts/jboss.container.wildfly.launch.elytron
        # Custom scripts from 'jboss.container.wildfly.launch.elytron' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.elytron/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.elytron:1.0'

###### START module 'jboss.container.wildfly.launch.keycloak:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.keycloak' module content
        COPY modules/jboss.container.wildfly.launch.keycloak /tmp/scripts/jboss.container.wildfly.launch.keycloak
        # Custom scripts from 'jboss.container.wildfly.launch.keycloak' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.keycloak/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.keycloak:1.0'

###### START module 'jboss.container.wildfly.launch.tracing:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.tracing' module content
        COPY modules/jboss.container.wildfly.launch.tracing /tmp/scripts/jboss.container.wildfly.launch.tracing
        # Custom scripts from 'jboss.container.wildfly.launch.tracing' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.tracing/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.tracing:1.0'

###### START module 'os-eap7-sso-adapters:7.4.5-kie'
###### \
        # Copy 'os-eap7-sso-adapters' module general artifacts to '/tmp/artifacts/' destination
        COPY \
            artifacts/rh-sso-7.4.5-eap7-adapter.zip \
            artifacts/rh-sso-7.4.5-saml-eap7-adapter.zip \
            /tmp/artifacts/
        # Copy 'os-eap7-sso-adapters' module content
        COPY modules/os-eap7-sso-adapters /tmp/scripts/os-eap7-sso-adapters
        # Custom scripts from 'os-eap7-sso-adapters' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/os-eap7-sso-adapters/configure.sh" ]
###### /
###### END module 'os-eap7-sso-adapters:7.4.5-kie'

###### START module 'jboss.container.wildfly.launch.deployment-scanner:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.deployment-scanner' module content
        COPY modules/jboss.container.wildfly.launch.deployment-scanner /tmp/scripts/jboss.container.wildfly.launch.deployment-scanner
        # Custom scripts from 'jboss.container.wildfly.launch.deployment-scanner' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.deployment-scanner/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.deployment-scanner:1.0'

###### START module 'jboss.container.wildfly.launch.extensions:1.0'
###### \
        # Copy 'jboss.container.wildfly.launch.extensions' module content
        COPY modules/jboss.container.wildfly.launch.extensions /tmp/scripts/jboss.container.wildfly.launch.extensions
        # Custom scripts from 'jboss.container.wildfly.launch.extensions' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.wildfly.launch.extensions/configure.sh" ]
###### /
###### END module 'jboss.container.wildfly.launch.extensions:1.0'

###### START module 'openshift-layer:1.0'
###### \
        # Copy 'openshift-layer' module content
        COPY modules/openshift-layer /tmp/scripts/openshift-layer
        # Custom scripts from 'openshift-layer' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/openshift-layer/configure_layers.sh" ]
###### /
###### END module 'openshift-layer:1.0'

###### START module 'openshift-passwd:1.0'
###### \
###### /
###### END module 'openshift-passwd:1.0'

###### START module 'jboss.container.prometheus.api:1.0'
###### \
###### /
###### END module 'jboss.container.prometheus.api:1.0'

###### START module 'jboss.container.prometheus.bash:1.0'
###### \
        # Copy 'jboss.container.prometheus.bash' module general artifacts to '/tmp/artifacts/' destination
        COPY \
            artifacts/jmx_prometheus_javaagent-0.3.2.redhat-00003.jar \
            /tmp/artifacts/
        # Copy 'jboss.container.prometheus.bash' module content
        COPY modules/jboss.container.prometheus.bash /tmp/scripts/jboss.container.prometheus.bash
        # Set 'jboss.container.prometheus.bash' module defined environment variables
        ENV \
            AB_PROMETHEUS_JMX_EXPORTER_CONFIG="/opt/jboss/container/prometheus/etc/jmx-exporter-config.yaml" \
            AB_PROMETHEUS_JMX_EXPORTER_PORT="9799" \
            JBOSS_CONTAINER_PROMETHEUS_MODULE="/opt/jboss/container/prometheus" 
        # Custom scripts from 'jboss.container.prometheus.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.prometheus.bash/configure.sh" ]
###### /
###### END module 'jboss.container.prometheus.bash:1.0'

###### START module 'jboss.container.eap.prometheus.agent:1.0'
###### \
        # Copy 'jboss.container.eap.prometheus.agent' module content
        COPY modules/jboss.container.eap.prometheus.agent /tmp/scripts/jboss.container.eap.prometheus.agent
        # Custom scripts from 'jboss.container.eap.prometheus.agent' module
        USER 185
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.eap.prometheus.agent/configure.sh" ]
###### /
###### END module 'jboss.container.eap.prometheus.agent:1.0'

###### START module 'jboss.container.eap.prometheus.config:7.2-kie'
###### \
        # Copy 'jboss.container.eap.prometheus.config' module content
        COPY modules/jboss.container.eap.prometheus.config /tmp/scripts/jboss.container.eap.prometheus.config
        # Custom scripts from 'jboss.container.eap.prometheus.config' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss.container.eap.prometheus.config/configure.sh" ]
###### /
###### END module 'jboss.container.eap.prometheus.config:7.2-kie'

###### START module 'os-eap-txnrecovery.bash:1.0'
###### \
        # Copy 'os-eap-txnrecovery.bash' module content
        COPY modules/os-eap-txnrecovery.bash /tmp/scripts/os-eap-txnrecovery.bash
        # Custom scripts from 'os-eap-txnrecovery.bash' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/os-eap-txnrecovery.bash/install_as_root.sh" ]
###### /
###### END module 'os-eap-txnrecovery.bash:1.0'

###### START module 'os-eap-txnrecovery.run:python3'
###### \
        # Copy 'os-eap-txnrecovery.run' module content
        COPY modules/os-eap-txnrecovery.run /tmp/scripts/os-eap-txnrecovery.run
        # Custom scripts from 'os-eap-txnrecovery.run' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/os-eap-txnrecovery.run/install_as_root.sh" ]
###### /
###### END module 'os-eap-txnrecovery.run:python3'

###### START module 'os-eap-python:3.6'
###### \
        # Copy 'os-eap-python' module content
        COPY modules/os-eap-python /tmp/scripts/os-eap-python
        # Switch to 'root' user to install 'os-eap-python' module defined packages
        USER root
        # Install packages defined in the 'os-eap-python' module
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y python36 \
            && microdnf clean all \
            && rpm -q python36
        # Custom scripts from 'os-eap-python' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/os-eap-python/configure.sh" ]
###### /
###### END module 'os-eap-python:3.6'

###### START module 'jboss-kie-common:1.0'
###### \
        # Copy 'jboss-kie-common' module content
        COPY modules/jboss-kie-common /tmp/scripts/jboss-kie-common
        # Custom scripts from 'jboss-kie-common' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss-kie-common/configure.sh" ]
###### /
###### END module 'jboss-kie-common:1.0'

###### START module 'jboss-kie-wildfly-common:1.0'
###### \
        # Copy 'jboss-kie-wildfly-common' module content
        COPY modules/jboss-kie-wildfly-common /tmp/scripts/jboss-kie-wildfly-common
        # Custom scripts from 'jboss-kie-wildfly-common' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss-kie-wildfly-common/configure.sh" ]
###### /
###### END module 'jboss-kie-wildfly-common:1.0'

###### START module 'jboss-kie-workbench:1.0'
###### \
        # Copy 'jboss-kie-workbench' module content
        COPY modules/jboss-kie-workbench /tmp/scripts/jboss-kie-workbench
        # Custom scripts from 'jboss-kie-workbench' module
        USER root
        RUN [ "sh", "-x", "/tmp/scripts/jboss-kie-workbench/configure.sh" ]
###### /
###### END module 'jboss-kie-workbench:1.0'

###### START image 'rhpam-7/rhpam-businesscentral-rhel8:7.11.0'
###### \
        # Copy 'rhpam-7/rhpam-businesscentral-rhel8' image general artifacts to '/tmp/artifacts/' destination
        COPY \
            jboss-eap-7.3.6-patch.zip \
            artifacts/rhpam_business_central_distribution.zip \
            artifacts/rhpam_business_central_monitoring_distribution.zip \
            artifacts/rhpam_add_ons_distribution.zip \
            artifacts/rhpam_kie_server_distribution.zip \
            artifacts/rhdm_add_ons_distribution.zip \
            artifacts/rhdm_decision_central_distribution.zip \
            artifacts/rhdm_kie_server_distribution.zip \
            artifacts/kie-server-services-jbpm-cluster-7.52.0.Final-redhat-00007.jar \
            /tmp/artifacts/
        # Switch to 'root' user to install 'rhpam-7/rhpam-businesscentral-rhel8' image defined packages
        USER root
        # Install packages defined in the 'rhpam-7/rhpam-businesscentral-rhel8' image
        RUN microdnf --setopt=install_weak_deps=0 --setopt=tsflags=nodocs install -y git \
            && microdnf clean all \
            && rpm -q git
        # Set 'rhpam-7/rhpam-businesscentral-rhel8' image defined environment variables
        ENV \
            CONFIG_ADJUSTMENT_MODE="xml" \
            HTTPS_ENABLE_HTTP2="true" \
            JBOSS_IMAGE_NAME="rhpam-7/rhpam-businesscentral-rhel8" \
            JBOSS_IMAGE_VERSION="7.11.0" \
            LOGGER_CATEGORIES="org.infinispan.client.hotrod.impl.protocol.Codec21:ERROR, org.infinispan.protostream.impl.AnnotatedDescriptorImpl:ERROR" 
        # Set 'rhpam-7/rhpam-businesscentral-rhel8' image defined labels
        LABEL \
            com.redhat.component="rhpam-7-businesscentral-rhel8-container"  \
            description="Red Hat Business Central 7.11 OpenShift container image"  \
            io.cekit.version="3.12.0.dev0"  \
            io.k8s.description="Platform for running Red Hat Business Central"  \
            io.k8s.display-name="Red Hat Business Central 7.11"  \
            io.openshift.expose-services="8080:http,8443:https"  \
            io.openshift.tags="javaee,eap,eap7,rhpam,rhpam7"  \
            name="rhpam-7/rhpam-businesscentral-rhel8"  \
            summary="Red Hat Business Central 7.11 OpenShift container image"  \
            version="7.11.0" 
        # Exposed ports in 'rhpam-7/rhpam-businesscentral-rhel8' image
        EXPOSE 8080 8443 8778
###### /
###### END image 'rhpam-7/rhpam-businesscentral-rhel8:7.11.0'



    # Switch to 'root' user and remove artifacts and modules
    USER root
    RUN [ ! -d /tmp/scripts ] || rm -rf /tmp/scripts
    RUN [ ! -d /tmp/artifacts ] || rm -rf /tmp/artifacts
    # Clear package manager metadata
    RUN microdnf clean all && [ ! -d /var/cache/yum ] || rm -rf /var/cache/yum

    # Define the user
    USER 185
    # Define the working directory
    WORKDIR /home/jboss
    # Define run cmd
    CMD ["/opt/eap/bin/openshift-launch.sh"]
## /
## END target image