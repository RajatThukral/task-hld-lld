# HLD+LLD Design Task

# Design Requirements

Consider a camera-module whose interactions are defined as follows:

1. the module can be asked to start capturing an image asynchronously
2. the module can register a success image callback from the user → the callback will receive a captured image
3. the module can register a failure image callback from the user → the callback will receive an error message stating the failure of the camera module to capture an image

Usage of the camera-module to capture an image:

1. a user should set a successful capture callback - which will get invoked on capture success
2. a user should set a failure capture callback - which will get invoked on capture failure
3. a user then submits a capture request
4. the user will have to wait on the success callback or the failure callback to be invoked
5. if success callback is invoked → the user will receive the captured image in the callback
6. if the failure callback is invoked → the user will receive the error emssage in the failure callback

---

# Properties of the Camera-System

Design a system which accepts concurrent capture-requests from different clients and returns the capture-result to each accepted capture-request.

The system uses the above described camera-module to actually capture the images; the following are the properties of the camera-system

1. any client can submit a capture-request to the camera-system
2. the client here can be any code-logic present in a system which has access to the camera-system
3. if a client has submitted a capture-request → it will wait for the capture-request to be serviced by the camera-system and then only, the control will be returned back by the camera-system to the client
4. the camera-system can accept multiple requests in parallel and it has to process all of them
5. the camera-system can have a way of measuring the urgency of the capture-request - how urgent is it to capture the image,
    for example, consider a self-driving car as a system which uses the camera-system,
    one client of the camera-system in the self-driving car could be an entity which captures the road-view for the purpose of logging the journey for the end-user to view later on;
    the other client of the camera-system could be the entity which uses the captured image to take steering decisions;
    so, for the latter client - the urgency is **higher** because they want to take steering decision and they want as minimum delay as possible between the time they requested the image and the time they got the image back, than, the former user-which only wants to capture the image for journey logging

6. the client of the camera-system can be aware of the other clients of the camera-system and the knowledge that there capture-request will be contended against other clients; therefore, they can supply some indication of the urgency of the request
7. the camera-system should understand the above sent indication by the client
8. the camera-system returns the capture-result for each capture-request
9. if the camera-request is successful, the capture-result would contain the captured image
10. if the camera-system encounters an error in capturing the image ⇒ the same error should be reflected in the capture-result
11. the responsibility of the camera-system is to service all requests and satisfy the urgency of all requests as efficiently as possible

---

# Deliverables

1. design of the camera-system with the camera-module needs to be done
2. the camera-module should remain abstracted without any specific logic
3. the camera-system should adhere to all the requirements mentioned above
4. design an HLD ⇒ the design document should contain
    1. responsibility of each block used in the HLD
    2. use-case diagram explaining the logical flow of events that happen when two requests with different urgency levels are concurrently submitted to the camera-system
5. design an LLD ⇒ the design document should contain
    1. proper classes/interfaces ready to be implemented
    2. use-case diagram explaining the logical flow of events that happen when two requests with different urgency levels are concurrently submitted to the camera-system
