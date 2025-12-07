# Linux Kernel
Linux Kernel, işletim sisteminin çekirdeğidir yani donanım ile yazılım arasında iletişimi kuran katmandır. 
- CPU, RAM, depolama, ekran, kamera, sensörler gibi tüm donanım bileşenlerini yönetir. Uygulamalar donanıma direkt erişemez, kernel aracılığıyla erişir.
- Her uygulamaya ne kadar RAM verileceğine karar verir, bellek izolasyonunu sağlar. Bir uygulamanın başka bir uygulamanın belleğine erişmesini engeller.
- Her uygulamayı kendi UID'si ile çalıştırır. Bu sayede uygulamalar birbirinden izole olur - Android'in sandbox yapısının temeli buradan gelir.

