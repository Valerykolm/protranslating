<template>
  <h1 class="text-center mt-3">List of clients</h1>
  <div class="container">
    <div class="row">
      <div class="col-md-auto">
        <table class="table">
        <thead>
          <tr>
            <th scope="col">Clients</th>
            <th scope="col"></th>
            <th scope="col"></th>
            <th scope="col" colspan="2"><button>New client</button></th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Phone</th>
            <th scope="col">Providers</th>
            <th scope="col"></th>
          </tr>
          <tr>
            <td>Test</td>
            <td>test@krfs.com</td>
            <td>305-555-0000</td>
            <td>Provider1, Provider3, Provider5</td>
            <td><a href="#">Edit</a></td>
          </tr>
          <tr>
            <td>Test1</td>
            <td>test1@krfs.com</td>
            <td>305-000-5555</td>
            <td>Provider3</td>
            <td><a href="#">Edit</a></td>
          </tr>
          <tr>
            <td>Test2</td>
            <td>test2@krfs.com</td>
            <td>305-333-5555</td>
            <td>Provider2, Provider4</td>
            <td><a href="#">Edit</a></td>
          </tr>
        </tbody>
      </table>
      </div>
    </div>
  </div>
</template>

<script>

</script>

<style src="./main.css"></style>
<style src="./bootstrap.min.css"></style>
