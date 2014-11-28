Due to ATS and C sharing the same semantics, it is possible for ATS to interface with Java through [JNI](http://en.wikipedia.org/wiki/Java_Native_Interface) (Java Native Interface). One area where this can be useful is in the [MVC](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) (Model-View-Controller) design pattern where the Controller and Model aspects will be well suited to ATS, where efficiency and precision are important, and the View (UI or GUI) can be implemented in Java, which has a diverse set of GUI APIs.

There is a [matrix example](../tree/master/doc/EXAMPLE/Java/matrix) using the MVC paradigm. Other [JNI examples](https://github.com/githwxi/ATS-Postiats-contrib/tree/master/contrib/JNI), including a minimal class in Java for linear arrays in ATS, may be found in [ATS contrib](Contrib). Small projects using Java in contrib include [GameOf24](https://github.com/githwxi/ATS-Postiats-contrib/tree/master/projects/SMALL/GameOf24) (which supports several other languages as well) and a [calculator](https://github.com/githwxi/ATS-Postiats-contrib/tree/master/projects/SMALL/Calculator).