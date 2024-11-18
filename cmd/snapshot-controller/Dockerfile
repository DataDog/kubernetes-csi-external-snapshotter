ARG BASE_IMAGE
ARG BUILDER_IMAGE

FROM $BUILDER_IMAGE as builder
WORKDIR /go/src/kubernetes-csi/external-snapshotter
ADD . .
ENV GOTOOLCHAIN auto
ENV GOFLAGS="-buildvcs=false"
RUN make build

FROM $BASE_IMAGE
LABEL maintainers="Compute"
LABEL description="Snapshot Controller"
ARG binary=./bin/snapshot-controller

COPY --from=builder /go/src/kubernetes-csi/external-snapshotter/${binary} snapshot-controller
ENTRYPOINT ["/snapshot-controller"]
