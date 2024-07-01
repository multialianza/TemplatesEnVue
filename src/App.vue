<template>
  <div id="app" class="appContainer p-5">
    <div class="p-5 text-center">
      <h1>Personaliza tu Contenido</h1>
    </div>

    <div class="container p-5">
      <div class="containerForm">
        <div>
          <label class="p-2" for="colorFondo">Color de fondo </label>
          <input type="color" id="colorFondo" name="colorFondo" v-model="colorFondo"><!--Input color de fondo-->
        </div>
        <div>
          <label class="p-2" for="colorTexto">Color de texto </label>
          <input type="color" id="colorTexto" name="colorTexto" v-model="colorTexto"><!--Input color de texto-->
        </div>
        <div>
          <label class="p-2" for="colorTexto">Mostrar texto </label><input type="checkbox" v-model="texto"><!--Checkbox para determinar si se debe mostrar el texto o no-->
        </div>
        <div>
          <label class="p-2" for="rangeBorder">Borde </label>
          <input type="range" id="rangeBorder" name="rangeBorder" min="0" max="50" step="1" v-model="radiusElement"><!--Input tipo range para selecionar el borde de un elemento con valor minimo 0 y máximo de 50-->
          <span>{{ radiusElement + "%" }}</span>
        </div>
        <div>
          <label class="p-2" for="textArea">Contenido textual</label><!--Textarea para ingresar y visualizar contenido textual-->
          <textarea class="form-control" placeholder="Escriba su comentario" id="textArea"
            v-model="textArea"></textarea>
        </div>
        <div>
          <label class="p-2" for="tipografia">Tipografía</label>
          <select name="tipografia" id="tipografia" v-model="tipografiaSeleccionada"><!--Select con opciones de tipografía de seleccionar la fuente de texto-->
            <option v-for="tipografia in tipografias" :key="tipografia.id" :value="tipografia.font">
              {{ tipografia.font }}</option>
          </select>
        </div>
        <div>
          <label class="p-2" for="opacidad">Opaco</label>
          <input type="checkbox" name="opacidad" id="opacidad" v-model="opacity"><!--Checkbox para determinar si el elemento debe ser opaco-->
        </div>
        <div>
          <label class="p-2" for="fontWeight">Tamaño de letras</label>
          <br>
          <input class="mx-2" type="radio" value="pequeño" v-model="tamañoLetra">Pequeño<!--Radio buttons para seleccionar el tamaño de la letra entre pequeño, mediano o grande-->
          <input class="mx-2" type="radio" value="mediano" v-model="tamañoLetra">Mediano
          <input class="mx-2" type="radio" value="grande" v-model="tamañoLetra">Grande
        </div>
      </div>

      <div class="containerElement">
        <div class="element" :style="{ backgroundColor: color2(), borderRadius: radiusElement + '%' }"><!--Esta directiva .class asigna dinamicamente una clase al párrafo dependiendo del valor de la variable tamañoLetra-->
          <div v-show="texto === true">
            <p :class="{ 'pequeño': tamañoLetra == 'pequeño', 'mediano': tamañoLetra == 'mediano', 'grande': tamañoLetra == 'grande' }"
              :style="{ fontFamily: tipografiaSeleccionada, color: colorTexto }">{{ textArea }}</p><!--Esta directiva :style asigna dinámicamente el tipo de fuente del texto y el color del texto-->
          </div>
        </div>
      </div>
    </div>


  </div>
</template>

<script>

export default {
  name: 'App',/*Indica el nombre del componente App */
  data() {      /*Retorna un objeto con varias propiedades, colorFondo, colorTexto, texto, etc. */
    return {
      colorFondo: "",
      colorTexto: "",
      texto: "",
      radiusElement: 0,
      textArea: "",
      opacity: false,
      tamañoLetra: "",
      tipografias: [          /*Es un array de objetos con propiedades id, name y font para almacenar opciones de tipografías */
        { id: 1, name: "Arial", font: "Arial" },
        { id: 2, name: "Lucida sans", font: "Lucida sans" },
        { id: 3, name: "Georgia", font: "Georgia" },
      ],
      tipografiaSeleccionada: "",

    }
  },
  methods: {    /*Es una función que convierte un color de formato hexagecimal a formato rgba, teneindo en cuenta la transparencia según el valor de la propiedad opacity */
    color2: function () {
      console.log(this.colorFondo)
      let red = parseInt(this.colorFondo.slice(1, 3), 16)
      let green = parseInt(this.colorFondo.slice(3, 5), 16)
      let blue = parseInt(this.colorFondo.slice(5, 7), 16)
      let transparencia = 0.7
      if (this.opacity) {
        transparencia = 1
      }
      console.log(red)
      return `rgba(${red},${green},${blue},${transparencia})`
    }
  },
  components: {   /*Se encuentra vacía pero se puede usar para importar y utilizar otros componentes dentro de éste */

  }
}
</script>

<style>
.appContainer {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}

.container {
  display: flex;
  justify-content: space-evenly;
  background-color: rgb(205, 130, 211);
  border-radius: 15px;
}

.element {
  width: 300px;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.pequeño {
  font-size: 1.5em;
}

.mediano {
  font-size: 2.5em;
}

.grande {
  font-size: 3.5em;
}
</style>
