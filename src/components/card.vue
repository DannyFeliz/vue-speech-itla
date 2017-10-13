<template>
<div class="col-md-8">
    <div class="card">
    <img class="card-img-top" :src="data.picture.large" alt="Card image cap">
    <div class="card-body">
        <h4 class="card-title">{{ data.name.first }} {{ data.name.last }}</h4>
        <h6 class="card-subtitle mb-2 text-muted">{{ data.email }}</h6>
        <p class="card-text">
            <table class="table">
                <thead>
                    <tr>
                        <th>Username</th>
                        <th>Email</th>
                        <th>Gender</th>
                        <th>Phone</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>{{ data.login.username }}</td>
                        <td>{{ data.email }}</td>
                        <td>{{ data.gender }}</td>
                        <td>{{ data.phone }}</td>
                    </tr>
                </tbody>
            </table>
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
    </div>
          <br>
      <br>

</div>
</template>

<script>
    export default {
        name: "Card",
        props: {
            data: {
                type: Object,
                required: true
            }
        },
        filters: {
            capitalize(text) {
                return text.charAt(0).toUpperCase() + text.slice(1);
            }
        }
    }
</script>