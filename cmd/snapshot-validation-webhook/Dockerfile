ARG BASE_IMAGE

FROM golang:1.20 as builder
WORKDIR /go/src/kubernetes-csi/external-snapshotter
ADD . .
ENV GOFLAGS="-buildvcs=false"
RUN make build

FROM $BASE_IMAGE
LABEL maintainers="Compute"
LABEL description="Snapshot Validation Webhook"
ARG binary=./bin/snapshot-validation-webhook

COPY --from=builder /go/src/kubernetes-csi/external-snapshotter/${binary} snapshot-validation-webhook
ENTRYPOINT ["/snapshot-validation-webhook"]
