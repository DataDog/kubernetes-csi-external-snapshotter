ARG BASE_IMAGE

FROM golang:1.21 as builder
WORKDIR /go/src/kubernetes-csi/external-snapshotter
ADD . .
ENV GOFLAGS="-buildvcs=false"
RUN make build

FROM $BASE_IMAGE
LABEL maintainers="Compute"
LABEL description="Snapshot Controller"
ARG binary=./bin/snapshot-controller

COPY --from=builder /go/src/kubernetes-csi/external-snapshotter/${binary} snapshot-controller
ENTRYPOINT ["/snapshot-controller"]
