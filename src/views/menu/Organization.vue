<template>
    <section>
        <CommonCRUD :columns="$store.state.classInfo.properties" apiRoot="/identity/organization"
                    :formColumns="formColumns">
        </CommonCRUD>
        <!--<CommonCRUD :columns="$store.state.classInfo.properties" apiRoot="/identity/sysClass" :formColumns="$store.state.classInfo.properties"></CommonCRUD>-->
    </section>
</template>

<script>
    import CommonCRUD from '@/components/CommonCRUD';
    export default {
        name: 'Organization',
        data() {
            return {
                formColumns: [],
            }
        },
        methods:{
            //父组织名称下拉项
            loadProjectOptions() {
                this.$http('POST', 'identity/organization/list', false).then(
                    data => {
                        this.formColumns.filter( item => item.name === 'parentId')[0].options = data.map(item => { return {value: item.id, label: item.name}});
                    }
                )
            },
        },
        components: {
            CommonCRUD
        },
        created() {
            this.formColumns = this.$store.state.classInfo.properties;
            this.loadProjectOptions();
        }
    }
</script>

<style scoped>

</style>
