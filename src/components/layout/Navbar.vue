<template>
    <q-layout-header class="row justify-start">
        <q-toolbar
        color="dark"
        :glossy="$q.theme === 'ios'"
        :inverted="$q.theme === 'ios'"
        >
        <q-btn-dropdown color="dark" label="Project" class="q-mr-md">
        <!-- dropdown content goes here -->
            <q-list link>
                <q-item>
                    <q-item-side icon="create_new_folder" inverted color="light" />
                    <q-item-main>
                    <q-item-tile label v-on:click="this.$router.forcereload()">Start new Project</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
                <q-item-separator inset />
                    <q-item>
                    <q-item-side icon="folder" inverted color="light" />
                    <q-item-main>
                    <q-item-tile label>Open project</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
                <q-item-separator inset />
                <q-item>
                    <q-item-side icon="save" inverted color="light" />
                    <q-item-main>
                    <q-item-tile label>Save project</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
                <q-item-separator inset />
                <q-list-header inset>Recent projects</q-list-header>
                <q-item>
                    <q-item-side icon="access_time" inverted color="light"/>
                    <q-item-main>
                    <q-item-tile label>Project_XYZ</q-item-tile>
                    <q-item-tile sublabel> (December 14, 2018)</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
                </q-list>
            </q-btn-dropdown>
            <q-btn-dropdown color="dark" label="Document" class="q-mr-md">
                <!-- dropdown content goes here -->
                <q-list link>
                <q-item>
                    <q-item-side icon="note_add" inverted color="light" />
                    <q-item-main>
                    <q-item-tile label>Import document</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
                <q-item-separator inset />
                    <q-item>
                    <q-item-side icon="save_alt" inverted color="light" />
                    <q-item-main>
                    <q-item-tile label>Export document</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
                <q-item-separator inset />
                <q-list-header inset>Recently used documents</q-list-header>
                <q-item>
                    <q-item-side icon="access_time" inverted color="light"/>
                    <q-item-main>
                    <q-item-tile label>Document_XYZ</q-item-tile>
                    <q-item-tile sublabel> (December 14, 2018)</q-item-tile>
                    </q-item-main>
                    <q-item-side right icon="info" color="amber" />
                </q-item>
            </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown color="dark" label="Workspace" class="q-mr-md">
            <!-- dropdown content goes here -->
            <q-list link>
            <q-item>
                <q-item-side icon="photo_size_select_small" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Select Area</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item>
                <q-item-side icon="rotate_right" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Rotate 90°</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
                <q-item-side icon="no_sim" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Cut</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
                <q-item-side icon="file_copy" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Copy</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
                <q-item-side icon="file_copy" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Paste</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
                <q-item-side icon="call_split" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Separate Page</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
                <q-item-side icon="merge_type" inverted color="light" />
                <q-item-main>
                <q-item-tile label>Merge Pages</q-item-tile>
                </q-item-main>
                <q-item-side right icon="info" color="amber" />
            </q-item>
            </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown color="dark" label="History" class="q-mr-md" />
        <q-toolbar-title>
            Wire©
            <div slot="subtitle">Designed in Germany</div>
        </q-toolbar-title>
        <q-btn
            flat
            dense
            round
            @click="rightDrawerOpen = !rightDrawerOpen"
            aria-label="Menu"
        >
            <q-icon name="menu" />
        </q-btn>
        </q-toolbar>
    </q-layout-header>
</template>

<script>
export default {
  name: 'Navbar',
  data () {
    return {
      rightDrawerOpen: this.$q.platform.is.desktop
    }
  }
}
</script>

<style>
</style>
