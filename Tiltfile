LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')
NAMESPACE = os.getenv("NAMESPACE", default='jellin-dev')

k8s_custom_deploy(
    'appsso-starter-java',
    apply_cmd="tanzu apps workload apply -f config/workload.yaml --update-strategy replace --debug --live-update" +
               " --local-path " + LOCAL_PATH +
               " --namespace " + NAMESPACE +
               " --yes --output yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload',
    live_update=[
      sync('./target/classes', '/workspace/BOOT-INF/classes')
    ]
)

k8s_resource('appsso-starter-java', port_forwards=["8080:8080"],
            extra_pod_selectors=[{'carto.run/workload-name': 'appsso-starter-java', 'app.kubernetes.io/component': 'run'}])
allow_k8s_contexts('aks.be7fd3a2.azuresa.tap-iterate-aks')
update_settings ( max_parallel_updates = 3 , k8s_upsert_timeout_secs = 60 , suppress_unused_image_warnings = None ) 
