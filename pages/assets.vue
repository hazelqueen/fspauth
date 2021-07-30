<template>
    <div class="container">
        <NavBar />
        <h1>My Assets</h1>
        <div class="row">
            <div class="col-6">
                <h5>List of Assets</h5>
                <ul class="list-group">
                    <li class="list-group-item list: group-item-action" v-for="asset in assets" :key="asset.id" @click="onSelected(asset)">
                        {{asset.name}} <span class="float-right">{{asset.value}}</span>
                    </li>
                </ul>
            </div>
            <div class="col-4">
                
                <AssetView :asset="selectedAsset" @saved="onChanges" @newAsset="onNew" @deleted="onChanges"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return{
            assets: [],
            selectedAsset: {}
        }
    },

    methods: {
        async getMyAssets() {
            await this.axios.get('/axios')
            .then((res)=>{
                if(res.status==200) {
                    this.assets = res.data
                }
            })
        },
        onChanges() {
            this.getMyAssets()
            this.selectedAsset = {}
        },
        onSelected(asset) {
            this.selectedAsset = asset
        },
        onNew() {
            this.selectedAsset = {}
        },
    },
    created() {
        this.getMyAssets()
    }
}
</script>

