FROM fluent/fluentd:v0.12
MAINTAINER sam.crang@gmail.com

WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.3.0/bin:$PATH

USER root
RUN apk --no-cache add sudo build-base ruby-dev && \

    sudo -u fluent gem install fluent-plugin-sumologic_output && \
    sudo -u fluent gem install fluent-plugin-rewrite-tag-filter && \
    sudo -u fluent gem install fluent-plugin-logit && \

    rm -rf /home/fluent/.gem/ruby/2.3.0/cache/*.gem && sudo -u fluent gem sources -c && \
    apk del sudo build-base ruby-dev

EXPOSE 24224

USER fluent
CMD exec fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT
