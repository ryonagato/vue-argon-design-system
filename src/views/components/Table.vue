<template>
    <section>
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <div class="card border-0 rounded shadow">
                        <div class="card-body">
                            <h4>Task List</h4>
                            <hr>
                            <router-link :to="{name: 'posts.create'}" class="btn btn-md btn-success">Add Task</router-link>

                            <table class="table table-striped table-bordered mt-4">
                                <thead class="thead-dark">
                                    <tr>
                                        <th scope="col">TITLE</th>
                                        <th scope="col">DESCRIPTION</th>
                                        <th scope="col">CATEGORY</th>
                                        <th scope="col">STATUS</th>
                                        <th scope="col">DUE DATE</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="task in tasks" :key="task.id">
                                    <td>{{ task.title }}</td>
                                    <td>{{ task.description }}</td>
                                    <td>{{ task.category }}</td>
                                    <td>{{ task.status ? 'Completed' : 'Pending' }}</td>
                                    <td>{{ task.due_date }}</td>
                                </tr>
                                </tbody>
                            </table>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import axios from "axios"
import { onMounted, ref } from "vue";

export default {
  data() {
    return {
      tasks: [],
      error: null
    };
  },
  mounted() {
    axios.get('http://localhost:3000/api/tasklist')
      .then(response => {
        this.tasks = response.data.data;
      })
      .catch(error => {
        this.error = error.message;
        console.error('Error fetching tasks:', error);
      });
  }
};
</script>
<style>
</style>