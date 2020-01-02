FROM s2i-do288-go
LABEL "io.openshift.s2i.build.source-location"="go-hello/src" \
      "io.k8s.display-name"="go-hello" \
      "io.openshift.s2i.build.image"="s2i-do288-go"

USER root
# Copying in source code
COPY upload/src /tmp/src
COPY .s2i/bin/run /usr/libexec/s2i/run
# Change file ownership to the assemble user. Builder image must support chown command.
RUN chown -R 1001:0 /tmp/src
RUN mkdir /.cache && mkdir /.cache/go-build
RUN chown -R 1001:0 /.cache/go-build

USER 1001
# Assemble script sourced from builder image based on user input or image metadata.
# If this file does not exist in the image, the build will fail.
RUN /usr/libexec/s2i/assemble
# Run script sourced from builder image based on user input or image metadata.
# If this file does not exist in the image, the build will fail.
CMD /usr/libexec/s2i/run
