<template>
    <div class="csv-uploader">
      <input type="file" multiple @change="handleFiles">
      <button @click="mergeFiles" :disabled="files.length === 0">Merge Files</button>
      <a :href="downloadfile" download="merged.csv" v-if="downloadfile">Download File</a>
    </div>
  </template>
  
  <script>
  import Papa from 'papaparse';
  
  export default {
    name: 'CsvUploader',
    data() {
      return {
        files: [],
        csvData: [],
        downloadfile: null,
      };
    },
    methods: {
      handleFiles(event) {
        this.files = Array.from(event.target.files);
        this.csvData = [];
        this.files.forEach((file) => {
          Papa.parse(file, {
            complete: (results) => {
              this.csvData.push(results.data);
            },
          });
        });
      },
      mergeFiles() {
        if (this.csvData.length === 0) {
          return;
        }
        const headers = this.csvData[0][0];
        const mergeData = [headers];
  
        this.csvData.forEach((data) => {
          data.slice(1).forEach((row) => {
            mergeData.push(row);
          });
        });
        const csv = Papa.unparse(mergeData);
        this.downloadfile = URL.createObjectURL(new Blob([csv], { type: 'text/csv' }));
      },
    },
  };
  </script>
  
  <style scoped>
  .csv-uploader {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  input {
    border: 1px solid #ccc;
    height: 100px;
    font-size: large;
    text-align: center;
    line-height: 100px;
    padding: 0 20px;
    box-sizing: border-box;
    margin-bottom: 10px; /* Space between input and buttons */
  }
  
  button {
    padding: 10px 20px;
    font-size: large;
    cursor: pointer;
  }
  
  a {
    padding: 10px 20px;
    font-size: large;
    cursor: pointer;
    text-decoration: none;
    color: blue;
  }
  
  a:hover {
    text-decoration: underline;
  }
  </style>
  