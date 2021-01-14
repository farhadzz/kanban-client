<template>
    <div class="w-100" style="margin-bottom: 10px">
            <div class="card">
                <div class="card-body">
                    <h5 class="card-title">{{ dataTask.name }}</h5>
                </div>
                    <ul class="list-group list-group-flush">
                        <li class="list-group-item">{{ dataTask.description }}</li>
                    </ul>
            <div class="card-body">
                <a href="#" class="card-link btn btn-outline-warning">Show Detail</a>
            </div>                      
        </div>
    </div>
</template>

<script>
export default {
    name: "TaskBody",
    props: ['dataTask']
}
</script>

<style>

</style>