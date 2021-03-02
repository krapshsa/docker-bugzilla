FROM ubuntu:18.04

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
            gcc \
            make \
            curl \
            wget \
            vim \
            apache2 \
            libmysqlclient-dev \
            tzdata \
            sendmail \
            ca-certificates \
            perl-*
RUN TZ=Asia/Taipei \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata
RUN PERL_MM_USE_DEFAULT=1 cpan -i DBD::mysql \
            CGI \
            DateTime \
            DateTime::TimeZone \
            Template \
            Email::Sender \
            Email::MIME \
            URI \
            List::MoreUtils \
            Math::Random::ISAAC \
            JSON::XS
RUN ln -sT /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/cgi.load
RUN mkdir -p /var/www/html
RUN wget https://ftp.mozilla.org/pub/mozilla.org/webtools/bugzilla-5.0.6.tar.gz -O /tmp/bugzilla-5.0.6.tar.gz; \
    tar zxvf /tmp/bugzilla-5.0.6.tar.gz -C /var/www/html; \
    mv /var/www/html/bugzilla-5.0.6 /var/www/html/bugzilla; \
    rm /tmp/bugzilla-5.0.6.tar.gz
RUN mkdir -p /var/www/html/bugzilla/skins/custom
COPY ./apache2.conf /etc/apache2/apache2.conf
COPY ./htaccess /var/www/html/bugzilla/Bugzilla/.htaccess
COPY ./htaccess /var/www/html/bugzilla/contrib/.htaccess
COPY ./htaccess /var/www/html/bugzilla/lib/.htaccess
COPY ./htaccess /var/www/html/bugzilla/t/.htaccess
COPY ./htaccess /var/www/html/bugzilla/template/.htaccess
COPY ./htaccess /var/www/html/bugzilla/xt/.htaccess
COPY ./htaccess /var/www/html/bugzilla/skins/custom/.htaccess

CMD ["apache2ctl", "-D", "FOREGROUND"]
