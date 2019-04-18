<template>
  <div class="container">
    <div class="row">
      <h3 class="mx-auto">Github Repo Compare</h3>
    </div>
    <div class="row">
      <div class="col">
        <input
          type="text"
          name=""
          value=""
          class="form-control"
          placeholder="Enter name of repository to compare"
          v-model="form.reponame"
          @keyup.enter="searchRepo"
        />
        <ul class="list-group">
          <li v-for="repo in searchResults" class="list-group-item">
            {{ repo.full_name }} ({{ repo.stargazers_count }})
            <button
              type="button"
              class="btn btn-sm btn-outline-danger"
              @click="remove(repo)"
              v-if="reposToCompare.map(repo => repo.id).includes(repo.id)"
            >
              Remove
            </button>
            <button
              v-else
              type="button"
              name="button"
              class="btn btn-sm btn-outline-success"
              @click="addToCompare(repo)"
            >
              Add to compare
            </button>
          </li>
        </ul>
      </div>
      <!-- Results -->
      <div class="col">
        <table class="table">
          <thead>
            <tr>
              <th>Name</th>
              <th>Starts</th>
              <th>Match</th>
              <th>Forks</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="repos in reposToCompare" :key="repos.id">
              <td>{{ repos.full_name }}</td>
              <td>{{ repos.stargazers_count }}</td>
              <td>{{ repos.watchers_count }}</td>
              <td>{{ repos.forks_count }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      form: {
        reponame: ""
      },
      searchResults: [],
      reposToCompare: []
    };
  },
  methods: {
    searchRepo() {
      let apiUrl = "https://api.github.com/search/repositories?q=";
      apiUrl = apiUrl + this.form.reponame;
      fetch(apiUrl)
        .then(response => response.json())
        .then(data => (this.searchResults = data.items));
    },
    addToCompare(repo) {
      this.reposToCompare.push(repo);
    },
    remove(repo) {
      const indexOfRepo = this.reposToCompare.indexOf(repo);

      this.reposToCompare.splice(indexOfRepo, 1);
    }
  }
};
</script>
