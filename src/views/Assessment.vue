<template>
    <div class="justify-center max-w-lg mt-10">
        <h1 class="font-extrabold tracking-tigh text-3xl leading-10">
            Fetch data
        </h1>
        <div class="mt-8">
            <section>
                <div class="mt-12">
                    <p>Fetch posts from jsonplaceholder api</p>
                    
                    <p class="pt-2">
                        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="submit">Fetch</button>
                    </p>
                </div>
                <div class="mt-9">
                    <table class="table-auto">
                        <thead>
                            <tr>
                                <th>userId</th>
                                <th>id</th>
                                <th>title</th>
                                <th>body</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(post) in posts">
                                <td>{{ post.userId }}</td> 
                                <td>{{ post.id }}</td>
                                <td>{{ post.title }}</td>
                                <td>{{ post.body }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </section>
        </div>
    </div>
    
</template>

<script>
import axios from 'axios';
import { useToast } from "vue-toastification";

export default {
  data() {
    return {
      posts: [],
      errors: [],
      selected: "posts"
    }
  },
  setup() {
      const toast = useToast();
      return { toast }
    },
  methods: {
      submit(event) {
          if(this.selected !== "") {
              axios.get(`http://jsonplaceholder.typicode.com/posts`)
                .then(response => {
                // JSON responses are automatically parsed.
                    this.posts = response.data
                    console.log(response.data);
                    this.toast.success("Successfully fetched!");
                })
                .catch(e => {
                    this.errors.push(e)
                })
          }
      }
  }
}
</script>