# light-vs-istio test
Compare light-4j service mesh plus with Istio service mesh in Kubernetes cluster

### Introduction

We have received too many questions on what is the difference between Light-4j and Istio and we feel that a in-depth comparison is needed to ensure people understand these two and choose the right microservices architecture. Both are trying to address the cross-cutting concerns at the platform level so that developers can focus on the business logic when implementing microservices. 

* Cross-cutting concerns

Light-4j is trying to address the cross-cutting concerns in the same JVM process in the request/response chain with middleware handlers. 

Istio is trying to address all cross-cutting concerns at the network level with sidecars. 

* Service to service communication

For service to service interaction with Istio in the cloud, your caller needs to interact with the local sidecar, the local sidecar interacts with the remote sidecar and the remote sidecar interacts with the callee. There are numeric serializations and deserializations in between so the performance will suffer a lot. That is the most complains on the Istio. 

Light-4j uses client-side service discovery to load balance between service instances. Once discovery is done, it connects to the target instance with HTTP/2 and cache the connection for a period of time. This gives the best performance for service to service communication. 

* Security

If you think about the security, we are protecting the business logic in a request/response chain and Istio is a sidecar which is further from your business logic. The question is if it is sufficient enough. Light-4j is like a bodyguard stand beside you and Istio is a security guy patrols the perimeter of your building. 

### Service Mesh

Istio is service mesh that address cross-cutting concerns with sidecars. It assumes that you can build your services with any language or framework without thinking about cross-cutting concerns. 

In most of the cases, light-4j resolves cross-cutting concerns in the request/response chain. If one of the service or client is not built with light-4j, we have provide the similar funcationality of service mesh called light-router and light-proxy. 

Light-router is designed for an alien client and bring it into the light ecosystem.

Light-proxy is designed for an alien service and bring it into the light ecosystem. 

Unlike the Istio, you only need light-router or light-proxy unless both client and service are not built on light-4j. 

### Which product to choose

The key decision making point is that if you are using Java for all your services, then light-4j is the best fit. If you have services built with different technology stacks, then light-router/light-proxy or Istio. 

### Test 1
