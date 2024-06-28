<template>
    <div>
        <h2>Usia Anda Saat Ini: </h2>
        <h5>{{ tanggalLahir }}</h5>
    </div>
</template>

<script>

export default {
    name: 'app',
    props: ["tanggalLahir"],
}
</script>

<style scoped></style>