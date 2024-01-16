FROM archmachina/ansible-base:0.2.1

COPY --chown=ansible:ansible "./playbook/requirements.txt" "./playbook/requirements.yml" \
  "./playbook/ansible.cfg"  /work/
COPY --chown=ansible:ansible ./playbook/exec/ /work/exec/
RUN /work/exec/exec ansible_setup /work

USER 0:0
RUN cd /usr/local/bin/ && curl -fsSL https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv5.1.1/kustomize_v5.1.1_linux_amd64.tar.gz | \
  tar -xzvf - kustomize
USER 1000:1000

COPY --chown=ansible:ansible ./playbook/ /work

ARG BUILD_VERSION
RUN echo "$BUILD_VERSION" > /version.txt

ENTRYPOINT [ "/work/entrypoint" ]
