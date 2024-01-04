# Tutorial 3: Matrici
Questo è il tutorial più importante di tutta la serie. Leggilo almeno 8 volte. 

## Coordinate omogenee
Finora abbiamo rappresentato un punto nello spazio come una terna (x,y,z). Se aggiungiamo una coordinata, passiamo in coordinate omogenee e, un punto nello spazio è rappresentato dal vettore (x,y,z,w). Se w vale 1, i precedenti 3 valori identificano la posizione nello spazio del punto. Se w vale 0 invece stiamo indicando una direzione nello spazio e non un punto in particolare. Ci torna comodo passare in coordinate omogenee in modo da utilizzare un'unica formula matematica per punti e direzioni. 

## Matrici di trasformazione
In Computer Graphics utilizzeremo matrici di trasformazione 4x4 che ci permetteranno di trasformare i nostri punti. Quindi, spesso, avremo una moltiplicazione (occhio che l'ordine conta, l'operazione tra matrici e vettori non è commutativa) tra matrici 4x4 e vettori di 4 componenti. 

A livello di codice per definire vettori e matrici e poter effettuare operazioni tra di loro usiamo la libreria glm:

    glm::mat4 myMatrix;
    glm::vec4 myVector;
    glm::vec4 transformedVector = myMatrix * myVector; // Again, in this order ! this is important.

Le matrici di trasformazione sono matrici 4x4 suddivise fondamentalmente in 2 parti. La "parte bassa", ossia l'ultima riga, è fissa e vale 0 0 0 1. La parte alta invece è composta da una matrice di rotazione 3x3 e da un parte x y z di traslazione. Se voglio traslare e ruotare un oggetto nello spazio rappresenterò questa informazione, ossia la posizione finale dell'oggetto, mediante una matrice di trasformazione e la applicherò all'oggetto. 

## Matrici di traslazione
Se voglio traslare un vettore di 10 in direzione X positiva, mi basterà definire la parte di traslazione della matrice di trasformazione come (10,0,0) e lasciare la matrice identità come matrice di rotazione:

    #include <glm/gtx/transform.hpp> // after <glm/glm.hpp>
    glm::mat4 myMatrix = glm::translate(glm::mat4(), glm::vec3(10.0f, 0.0f, 0.0f));
    glm::vec4 myVector(10.0f, 10.0f, 10.0f, 0.0f);
    glm::vec4 transformedVector = myMatrix * myVector; // guess the result

## Scalare un vettore
Se vogliamo scalare un vettore in tutte e 3 le direzioni basta mettere la quantità di scala sulla diagonale della matrice di rotazione, all'interno della matrice di trasformazione e lasciare la parte di traslazione nulla. 

## Matrici di rotazione
    // Use #include <glm/gtc/matrix_transform.hpp> and #include <glm/gtx/transform.hpp>
    glm::vec3 myRotationAxis( ??, ??, ??);
    glm::rotate( angle_in_degrees, myRotationAxis );

## Cumulating transformations
Quindi, ricapitolando, abbiamo visto come ruotare, traslare e scalare un vettore utilizzando calcoli tra il vettore ed una matrice opportunamente definita. Per ruotare un vettore gli dovrò dare una matrice di rotazione non nulla, per traslarlo gli dovrò dare un set di traslazione non nullo e per scalarlo dovrò popolare la diagonale principale della matrice di rotazione della quantità di scala. Il tutto è relativo alla matrice di trasformazione, la quale contiene sia parte di rotazione che di traslazione. Per ottenere un risultato unico basta combinare tra loro queste matrici:

    TransformedVector = TranslationMatrix * RotationMatrix * ScaleMatrix * OriginalVector;

## The Model, View and Projection matrices
Le matrici di model, view e projection è un modo pulito di suddividere le trasformazioni. 
### The Model matrix
Qualsiasi oggetto grafico, 2D o 3D, è definito come un set di vertici. Ogni vertice è definito dalle 3 coordinate x, y e z. Tutto è riferito rispetto al sistema di riferimento centrale dell'oggetto, quindi se un vertice avrà coordinate (0,0,0), allora quel vertice coinciderà con il centro dell'oggetto. Se vogliamo muovere il nostro oggetto, ad esempio perchè magari è controllato tramite mouse e tastiera, questo, matematicamente, si tradurrà in un calcolo tra matrici e vettori. In particolare, ad ogni frame, ogni vertice verrà trasformato, ossia verrà moltiplicato per una matrice di trasformazione. Alla fine di questo calcolo, all'interno del frame, avremo tutti i vertici che sono stati trasformati, ossia vederemo l'oggetto che si è spostato rispetto alla posizione precedente. 

Quindi, siamo passati da un oggetto che era definito rispetto al suo centro, ad un oggetto che è definito nello spazio. Siamo passati al World Space. Siamo passati dal Model Space al World Space. Nel Model Space tutti i vertici sono definiti rispetto al centro del mondo che, in prima battuta, corrisponde con il centro dell'oggetto. Nel World Space tutti i vertici dell'oggetto sono definiti rispetto al centro del mondo, ossia il centro della scheda grafica.

### The View matrix
Se vogliamo vedere una montagna da un'angolazione diversa possiamo muovere la camera e tenere ferma la montagna o, tenere ferma la camera e muovere la montagna. Questo è ovviamente impossibile nella realtà ma viene facile in Computer Graphics. 

All'inizio la camera è al centro del mondo. Supponiamo di voler muovere la camera di 3 unità positive lungo X. Questo è equivalente a muovere il mondo di 3 unità negative verso X. Quindi, di fatto la camera la teniamo ferma e muoviamo il resto del mondo:

    glm::mat4 ViewMatrix = glm::translate(glm::mat4(), glm::vec3(-3.0f, 0.0f ,0.0f));

### The Projection matrix
Un punto sullo schermo non è definito soltanto dalle coordinate (x,y). Ad esempio, abbiamo detto che il punto (0,0) si trova al centro dello schermo. In realtà, conta anche il valore Z, ossia quanto il punto è distante dalla camera. Ad esempio, il punto (10,10,10) risulterà più vicino al centro dello schermo rispetto al punto (10,10,5). Questo a causa della prospettiva. Quindi, lo stesso punto di coordiante (x,y) può risultare più o meno vicino al centro dello schermo a causa della prospettiva. La prospettiva è rappresentata da una matrice 4x4

# Tutorial 4: Un Cubo Colorato