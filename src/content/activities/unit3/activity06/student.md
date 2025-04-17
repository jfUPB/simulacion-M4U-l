**¿Por qué multiplicamos la aceleración por cero al final de cada frame?**

El propósito de multiplicar la aceleración por cero al final de cada frame es "resetear" la aceleración. Al principio de cada frame, la aceleración debe reflejar solo las fuerzas actuales que actúan sobre el objeto. Si no reseteamos la aceleración, la aceleración acumulada de frames anteriores seguiría sumándose, lo que daría como resultado una aceleración superior a esperada.
