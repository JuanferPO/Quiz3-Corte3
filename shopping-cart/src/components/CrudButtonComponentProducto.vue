<!-- CrudButtonComponent.vue -->
<template>
  <div>
    <ButtonComponent id="find" value="Consultar todo" expand="full" color="warning" nameMethod="findAllRecords" @click="handleClickFind"/>    
    <ButtonComponent id="created" value="Agregar" expand="full" color="warning" nameMethod="createRecord" @click="handleClickCreate"/>
    <ButtonComponent id="updated" value="Modificar" expand="full" color="warning" nameMethod="updateRecord"  @click="handleClickUpdate"/>
    <ButtonComponent id="deleted" value="Eliminar" expand="full" color="warning" nameMethod="deleteRecordPhysical" @click="handleClickDelete" />    
    <ButtonComponent id="deletedLogical" value="Eliminar lógicamente" expand="full" color="warning" nameMethod="deleteRecordLogical" @click="handleClickDeleteLogical" />    
  </div>
</template>

<script setup lang="ts">
  import ButtonComponent from '@/components/ButtonComponent.vue';
  import axios from 'axios';
// Rutas de la API
const baseURL = 'http://localhost:8080/shopping_car/api/producto';

  // Método para manejar el clic en el botón de crear
  const handleClickCreate = () => {
    createRecord();
  };

  // Método para manejar el clic en el botón de actualizar
  const handleClickUpdate = () => {
    updateRecord(id, data);
  };

  // Método para manejar el clic en el botón de eliminar
  const handleClickDelete = () => {
    deleteRecordPhysical(id);
  };

  // Método para manejar el clic en el botón de eliminar lógicamente
  const handleClickDeleteLogical = () => {
    deleteRecordLogical(id);
  };

  // Método para manejar el clic en el botón de consultar
    const handleClickFind = () => {
      findAllRecords();
  };

// Métodos para interactuar con la API
// Obtener todos los registros
async function findAllRecords() {
  try {
    const response = await axios.get(baseURL);
    return response.data;
  } catch (error) {
    console.error('Error al obtener todos los registros:', error);
    throw error;
  }
}

// Obtener por ID
async function fetchRecordById(id) {
  try {
    const response = await axios.get(`${baseURL}/${id}`);
    return response.data;
  } catch (error) {
    console.error('Error al obtener el registro por ID:', error);
    throw error;
  }
}

// Crear registro
async function createRecord() {
  const data = {
    codigo: codigo.value,
    nombre: nombre.value,
    marca: marca.value,
    precio: precio.value,
    stock: stock.value
  };

  try {
    const response = await axios.post(baseURL, data);
    console.log('Registro creado exitosamente:', response.data);
  } catch (error) {
    console.error('Error al crear el registro:', error);
  }
}


// Actualizar registro
async function updateRecord(id, data) {
  try {
    const response = await axios.put(`${baseURL}/${id}`, data);
    return response.data;
  } catch (error) {
    console.error('Error al actualizar el registro:', error);
    throw error;
  }
}

// Eliminar registro físico
async function deleteRecordPhysical(id) {
  try {
    const response = await axios.delete(`${baseURL}/${id}`);
    return response.data;
  } catch (error) {
    console.error('Error al eliminar el registro físico:', error);
    throw error;
  }
}

// Eliminado lógico
async function deleteRecordLogical(id) {
  try {
    const response = await axios.put(`${baseURL}/delete-logical/${id}`);
    return response.data;
  } catch (error) {
    console.error('Error al realizar el eliminado lógico:', error);
    throw error;
  }
}


</script>

<style scoped src="../theme/container.css"></style>
