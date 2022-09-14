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
  ### - Unit Test
  - Despues de haber visto las fuentes de codigos, pudimos ver lo siguiente:
  
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
  ### - 
   
