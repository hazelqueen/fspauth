<template>
    <div>
        <button class="btn btn-success float-right" @click="onNew">
            New Asset
        </button>
        <h5>Asset View</h5>

        <hr>

        <form action="" @submit.prevent="onSave">

            <b-form-group label="Name">
                <b-form-input v-model="asset.name"></b-form-input>
            </b-form-group>

            <b-form-group label="Description">
                <b-form-input v-model="asset.description"></b-form-input>
            </b-form-group>
            
             <b-form-group label="Location">
                <b-form-input v-model="asset.location"></b-form-input>
            </b-form-group>

             <b-form-group label="Value">
                <b-form-input v-model="asset.value"></b-form-input>
            </b-form-group>

             <b-form-group label="Date Acquired">
                <b-form-input type="date" v-model="asset.acquired_on"></b-form-input>
            </b-form-group>

             <b-form-group label="Status">
                <b-form-input v-model="asset.status"></b-form-input>
            </b-form-group>

            <b-form-group>
                <button class="btn btn-primary" type="submit">Save Changes</button>
                <button class="btn btn-danger" type="button" @click="onDelete" v-if="asset.id">Delete</button>
            </b-form-group>

        </form>
    </div>
</template>

<script>
export default {
    props: {
        asset: {}
    },
    methods: {
        async onSave() {
            try {
                if(!this.add.id) {
                //new asset
                    await this.axios.post('/assets', this.asset)
                }else {
                //update asset
                    await this.axios.put('/assets/' + this.asset.id, this.asset)

            }

            this.$emit('saved');
            }catch(err) {
                alert(err.response.data.message)
            }
        },
        onNew() {
            this.$emit('newAsset')
        },
        async onDelete() {
            try {
                this.$axios.delete('/assets/' + this.asset.id)
            this.$emit('deleted')
            }catch(err) {
                alert(err.response.data.message)
            }
            
        }
    }
}
</script>