<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">Riwayat Kunjungan</h2>
                <div class="my-3">
                    <input type="search" class="form-control form-control-lg rounded-5" placeholder="Mencari" />
                </div>
                <div class="my-3 text-muted">
                    <table class="table">
                        <thead>
                            <tr>
                                <td>No</td>
                                <td>Tanggal/Waktu</td>
                                <td>Nama</td>
                                <td>Keanggotaan</td>
                                <td>Tingkat</td>
                                <td>Jurusan</td>
                                <td>Kelas</td>
                                <td>Keperluan</td>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(visitor, i) in visitors" :key="i">
                                <td>{{ i + 1 }}</td>
                                <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
                                <td>{{ visitor.nama }}</td>
                                <td>{{ visitor.Keanggotaan.nama }}</td>
                                <td>{{ visitor.tingkat }}</td>
                                <td>{{ visitor.jurusan }}</td>
                                <td>{{ visitor.kelas }}</td>
                                <td>{{ visitor.Keperluan.nama }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
        <div class="d-grid gap-2 d-md-flex justify-content-md-strat">
            <nuxt-link to="/pengunjung/menu">
                <button type="submit" class="btn btn-light btn-lg rounded-5 px-5 me-md-2 mt-4">Menu</button>
            </nuxt-link>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient();

const visitors = ref([]);
const getPengunjung = async () => {
    const { data, error } = await supabase.from("Pengunjung").select(`*, Keanggotaan(*), Keperluan(*)`);
    if (data) visitors.value = data;
};
onMounted(() => {
    getPengunjung();
});
</script>

<style scoped>
.container-fluid {
    background-color: #4377de;
}
h2 {
    color: #fff;
}
</style>