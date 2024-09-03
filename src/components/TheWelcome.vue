<template>
  <div>
    <h1>Lista de Películas</h1>
    <table>
      <thead>
        <tr>
          <th>Poster</th>
          <th>Título</th>
          <th>Calificación</th>
          <th>IMDB</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pelicula in peliculas" :key="pelicula.id">
          <td>
            <img :src="pelicula.image || placeholderImage" :alt="pelicula.title" width="50" />
          </td>
          <td>{{ pelicula.movie }}</td>
          <td>{{ pelicula.rating }}</td>
          <td>
            <a :href="pelicula.imdb_url" target="_blank">Ver en IMDB</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      peliculas: [], // Array para almacenar las películas
      placeholderImage: 'ruta/placeholder.jpg', // Imagen de marcador de posición
    };
  },
  created() {
    // Hacer la solicitud a la API cuando el componente es creado
    this.obtenerPeliculas();
  },
  methods: {
    async obtenerPeliculas() {
      try {
        const response = await fetch("https://dummyapi.online/api/movies");
        const data = await response.json();
        this.peliculas = data; // Asignar los datos obtenidos al array de películas
        console.log(data  );
        
      } catch (error) {
        console.error("Error al obtener las películas:", error);
      }
    },
  },
};
</script>

<style scoped>
/* Estilos para la tabla */
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #000000;
}
th {
  background-color: #000000;
}
img {
  border-radius: 8px;
}
</style>


