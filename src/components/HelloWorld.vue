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
          <li class="list-group-item">Something</li>
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
            <tr></tr>
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
      searchResults = [];
    };
  },
  methods: {
    searchRepo() {
      let apiUrl = "https://api.github.com/search/repositories?q=";
      apiUrl = apiUrl + this.form.reponame;
      fetch(apiUrl)
        .then(response => response.json())
        .then(data => (
          this.searchResults = data.items;
        ));
    }
  }
};
</script>
