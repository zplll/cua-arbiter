{% verbatim %}
<template id="menuIconButton">
    <div id="menu-icon-button">
        <mu-icon-button icon="apps" slot="right" ref="appIcon" @click="appMenuToggle"></mu-icon-button>
        <mu-popover v-if="usernameAbbreviation!=null" :anchor-origin='{"vertical":"bottom","horizontal":"middle"}'
                    :target-origin='{"vertical":"top","horizontal":"middle"}' :trigger="appMenuTrigger"
                    :open="appMenuOpen" @close="appMenuHandleClose">
            <mu-menu>
                <mu-menu-item title="用例导入" left-icon="add"
                              @click="openImportDialog"></mu-menu-item>
                <mu-menu-item href="/arbiter/" title="用例管理" left-icon="mode_edit"></mu-menu-item>
                <mu-menu-item href="/arbiter/wholog/index.html" title="日志查询" left-icon="history"></mu-menu-item>
            </mu-menu>
        </mu-popover>
        <mu-dialog :open="dialog" title="用例导入" @close="closeImportDialog">
            <mu-text-field v-if="gitCloneStatus == 'finish'" icon="link" v-model="gitUrlPrefix"
                           label="git仓库的URL（例：https://github.com/shimine/cua-caseobjdemo.git）" :width="100"
                           label-float></mu-text-field>
            <mu-flat-button v-if="gitCloneStatus == 'finish'" slot="actions" @click="closeImportDialog" primary
                            label="取消"></mu-flat-button>
            <mu-flat-button v-if="gitCloneStatus == 'finish'" slot="actions" @click="cloneCaseObj" primary
                            label="导入"></mu-flat-button>
            <mu-linear-progress v-if="gitCloneStatus == 'running'" :size="10" color="blue"></mu-linear-progress>
        </mu-dialog>
    </div>
</template>
{% endverbatim %}