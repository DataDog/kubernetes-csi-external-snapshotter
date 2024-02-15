ARG BASE_IMAGE

FROM golang:1.21 as builder
WORKDIR /go/src/kubernetes-csi/external-snapshotter
ADD . .
ENV GOFLAGS="-buildvcs=false"
RUN make build

FROM $BASE_IMAGE
LABEL maintainers="Compute"
LABEL description="CSI External Snapshotter Sidecar"
ARG binary=./bin/csi-snapshotter

COPY --from=builder /go/src/kubernetes-csi/external-snapshotter/${binary} csi-snapshotter
ENTRYPOINT ["/csi-snapshotter"]
