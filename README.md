# Parcial_CVDS
## 1. GIT
  ### - Fork
  - El repositorio que vamos a trabajar se encuentra en el siguiente link de [GITHUB](https://github.com/DanielOchoa1214/Tetris.git)
  - Para poder trabajar con este repositorio debemos hacer un fork, ya que el repositorio original no podemos modificar.
  
  ![image](https://user-images.githubusercontent.com/77862048/190240776-5ce0bca6-715d-4b50-a72f-7af4e17f5f41.png)

  - Como podemos observar nos aparece la opción de hacer fork desde el repositorio original.
  
  ![image](https://user-images.githubusercontent.com/77862048/190241172-c1faa7dc-95b0-4412-8896-d627ff26afc1.png)

  - En esta imagen se puede observar que un nuevo repositorio se creo en el GITHUB donde trabajaremos.
  
  ![image](https://user-images.githubusercontent.com/77862048/190241397-fb33fa96-7b25-4cb4-a15f-89fc12213a2f.png)

  - Ademas podemos observar desde el repositorio de nuestro GITHUB desde donde se hizo el fork.
  ### Clone
  - Despues de hacer el fork debemos clonar el repositorio remoto al local.
  
  ![image](https://user-images.githubusercontent.com/77862048/190242380-0f746e2d-2b9c-4bb0-9314-64803b45f8dc.png)

  - Como vemos en la imagen hacemos clone desde el repositorio remoto y lo ponemos en la carpeta "ParcialTercioUno"
  
## 2. Identificando malas practicas
  ### - SOLID
   - Mirando los códigos de la capa de dominio pudimos observar un incupmlimiento al principio de SOLID especificamente a la L.
   - 
      ![image](https://user-images.githubusercontent.com/77862048/190265165-4f2b0a7c-753f-43e8-8e74-5ad6c0ac298d.png)
      
   - Mirando el diagrama de clases podemos observar que Board posee dos clases hijas. La clase SlowBoard practicamente no posee logica segun este diagrama.
   - 
      ![image](https://user-images.githubusercontent.com/77862048/190265318-ddc6a0ea-38e5-42d9-98e0-e9e035e3ba35.png)
      
   - Esto se ve reflejado en el código donde solo vemos al constructor de la clase.
     * El funcionamiento de cada clase es el siguiente:
        1. La clase Board es una clase abstracta que posee la lógica principal para el movimiento de las fichas.
        2. La clase AcceleratedBoard debe hacer que las fichas caigan mas rapido despues de cierto tiempo
        3. La clase SlowBoard se caracteriza por tener la velocidad constante
   - Teniendo en cuenta el funcionamiento de cada clase pudimos observar que el método "resume()" tenia una particularidad.

      ![image](https://user-images.githubusercontent.com/77862048/190266129-0a65d406-ca27-4001-a934-570cea30ff67.png)
      
      ![image](https://user-images.githubusercontent.com/77862048/190266821-1c3209b4-3f33-47c9-a108-c899da989523.png)

   - La varible fallingVelocity no tiene sentido en el caso que el tablero sea lento, eso quiere decir que la logica de este metodo no deberia estar en la clase padre por cuestiones de funcionamiento ya descritos. Esto se resolveria haciendo que cada clase hija haga su propia logica que cumpla con sus funcionalidades.
      
  ### - Unit Test
  - Despues de haber visto las fuentes de los test, pudimos ver lo siguiente:
  
  ![image](https://user-images.githubusercontent.com/77862048/190246931-35711e5a-9379-42a1-8717-3b50eaf0a5df.png)

  - Se puede observar que:
      1. No cumple con el nombramiento de las pruebas unitarias
      2. No cumple con el AAA
      3. No cumple con el principio FIRST.
  - Para solucionar esta mala practica deberiamos hacer lo siguiente:
      - Las clases de equivalencia que vemos en este test serian:
          - Limite inferior = Null
          - Nombre Valido = esta entre {"", "Gerber", "SuperJose", "Dano", "ManlyManChad", "GirlyGirlGina"}
          - Nombre Invalido = cualquier nombre que no este dentro de la lista ya dicha
  ```
  
    @Test
    public void give_unUsuario_when_esteSeaUnUsuarioExistenteGerber_then_colorDelUsuarioEsRojo() {
        //Arrange
        TetrisGUI.User = Null;
        try {
            //Act
            player = new HumanPlayer("dominio.SlowBoard");
            fail("No lanzo la excepcion")
        catch (TetrisException e) {
            //Assert
            assertEquals(e.getMessage(), TetrisException.NULL_USER);
        }
    }
    
    @Test
    public void give_unUsuario_when_esteSeaUnUsuarioExistenteGerber_then_colorDelUsuarioEsRojo() {
        //Arrange
        TetrisGUI.User = "Gerber";
        //Act
        player = new HumanPlayer("dominio.SlowBoard");
        //Assert
        assertEquals(player.getBackgroundColor(), new Color(153, 0, 0));
    }
    
    @Test
    public void give_unUsuario_when_esteSeaUnUsuarioExistenteGerber_then_colorDelUsuarioEsRojo() {
        //Arrange
        TetrisGUI.User = "Federico";
        try {
            //Act
            player = new HumanPlayer("dominio.SlowBoard");
            fail("No lanzo la excepcion")
        catch (TetrisException e) {
            //Assert
            assertEquals(e.getMessage(), TetrisException.INVALID_USER);
        }
    }
    
  ```
  ###
   
