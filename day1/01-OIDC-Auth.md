## Notes

Authentication vs Authorization
- Is the user who they say they are
- standards: 
    - saml
    - oauth2
- provided with auth0, cognito, etc.

Authorization
- no real standards
- no real developer services
- this means everyone rolls their own
    - problems with that
        - bad security
        - inconsistency
        - opportunity cost (if you have to build this stuff, that's time you can't spend doing other things)
        - broken access control is a serious problem (owasp top 10)

presenter is working in the authorization space to try to solve those problems for AuthZen.

large tech vendors are moving into the authorization space
- google zanzibar
- intuit authz
- carta authz4
- netflix product access service
- airbnb himeji3

Now we have enough to democratize this

### Old-school vs Cloud native authorization

OS
- What: Coarse grained
- How: Auth spaghetti logic
- When: Permission evaluated at runtime, scopes embedded in access token
    - immediately becomes stale ... what if authorization is revoked after the token is minted?

CN
- What: fine grained
    - Authorizing at the level of the resource
    - Old example of this: Unix ACLs
    - Newer example: RBAC ... roles assigned to users ... good, but led to role/group explosion
    - Attribute-based Access Control (ABAC) ... XACML ... an XML-based spec that specified who could access what and when. Based on attributes of users, applications, etc.
    - Relationship-Based Access Control (ReBAC) ... Model permissions as a set of relationships between different objects. ... Google docs based on this. More intuitive.
- How: Policy-based: authorization logic pulled out of app and baked into documents
    - Example: Rego ... AWS policy documents are very much similar and in this space.
    - Application code uses middleware to call authz service give a simple t/f y/n answer
    - Policies can be checked into source control and managed
- When: realtime
    - does this object have this permission on this resource right now?
    - authorize locally - you don't want an auth decision to take a lot of time
        - in same k8s cluster. 
        - physically close to the app
    - managed centrally - i.e. in a k8s control plane
        - policy as code distributed to authorizers when they are spun up


### Players
ABAC ---------------- | ---------------- ReBAC
xacml    alfa     *authzen*  zanzibar    ngac

[authzen charter](https://openid.net/wg/authzen)

personal note
layer 3 network layer
layer 4 transport layer
layer 7 application layer

authzen is a _spec_. It's a contract for interacting between an authorization decision maker and app code
    - there are required parts of this spec that is based on the work of others that have come before
can be serialized into protobufs or json
in goes payload to spec, back comes decision to spec

[authzen-interop.net](https://authzen-interop.net) ... an example site
[simple todo example](https://todo.authzen-interop.net) ... a working demo site

[github.com/openid/authzen](https://github.com/openid/authzen) ... proposed standard, cloneable repo



